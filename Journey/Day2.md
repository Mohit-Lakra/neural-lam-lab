 ### What I set out to do
  Finish the “automatic documentation” project: I wanted AutoAPI to actually generate the API pages and prove that our
  GitHub Actions job can build and deploy them. Until today the “API Reference” link just looped back to the intro page,
  so this felt pretty broken.

  ### What I dug into
  - Ran `pdm run jupyter-book build docs/ --all` and watched the logs. Found the culprit: AutoAPI was trying to parse
  every module but astroid 4.x now insists on an `AstroidBuilder(manager=…)`. The version bundled with AutoAPI v3 still
  does `AstroidBuilder()` with no arguments, so the parser crashes and silently gives us an empty toctree.
  - Looked at AutoAPI’s templates to confirm why the landing page was blank; with no top-level `neural_lam` object
  rendered, the `index.rst` toctree doesn’t list anything.
  - Re-read `.github/workflows/docs.yml` to make sure CI already runs `jupyter-book` and pushes to Pages. It does — the
  only blocker was AutoAPI falling over.

  ### What I actually changed
  - Wrote a tiny Sphinx extension `docs/scripts/autoapi_astroid_patch.py`. It monkey-patches Astroid’s builder to inject
  a default `AstroidManager` when AutoAPI calls it. Registered it via `docs/_config.yml`.
  - Switched `autoapi_add_toctree_entry` back on so AutoAPI writes `autoapi/index.rst`. Since `_toc.yml` already links to
  that file, the sidebar now shows every module automatically.
  - Nuked `docs/_build` and `docs/autoapi`, reran the build, and verified we finally have `docs/_build/html/autoapi/
  index.html` with the full module tree listed. The remaining warnings are just missing content (installation/usage
  pages, a README link in the notebook), not broken tooling.
  - Double-checked the docs workflow: pushes to `main` or `Auto-doc` will rebuild and deploy now that AutoAPI isn’t
  crashing.

  ### Where things stand
  - Auto-generated API docs are back: every module under `neural_lam` renders to HTML, so clicking “API Reference”
  actually goes somewhere.
  - CI will pick this up once I commit `docs/_config.yml` and the new extension and push; the GitHub Pages job should
  then publish automatically.
  - This is a solid prototype: the automation is solved, even if the content is still bare-bones.

  ### Still to do / ideas
  - Create real `docs/installation.md` and `docs/usage.md` (or remove those links). Same for the notebook’s `../README`
  reference.
  - Improve docstrings so the generated pages read well. Maybe add overview chapters (tutorials, usage guides) so the
  site isn’t just a raw API dump.
  - Consider customizing AutoAPI’s templates to give prettier module summaries.
