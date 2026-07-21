# easypng GitHub Action

Composite GitHub Action wrapping `npx easypng` (the npm package, source at
`amanghuman/easypng-cli`). Listed on the GitHub Marketplace. Companion to the browser tool at
`amanghuman.com/easypng.html` (source: `sanitizemeta/AmanGhuman`). See `CLAUDE.md` in
`sanitizemeta/AmanGhuman` for the full picture across all three pieces, this file is a pointer,
not the full story.

Owned by GitHub account `amanghuman`, not `sanitizemeta`. Run `gh auth switch --hostname
github.com --user amanghuman` before pushing here if another account is active
(`gh auth status` to check).

Versioned independently from the npm package (tags `v1`, `v1.0.0`, `v1.0.1`, and so on), since
this tracks changes to the CI wrapper YAML, not the compression logic. `v1` is a moving pointer
kept at the latest `v1.x` release: after cutting a new release, move it forward with
`git tag -f v1 && git push origin v1 --force`. The Marketplace listing's icon/branding can lag
behind a new release by some indeterminate amount of caching, don't assume a fix didn't work just
because the listing page hasn't updated yet.

`.github/workflows/test.yml` self-tests the action on every push, exercising both the success
path and the `--max-size` failure path. Check it passes before considering any action.yml change
done.

Never publish/tag a release without the user explicitly asking in that turn, even if they
approved a previous one, that approval doesn't carry forward.

Standing content rules: never mention Claude Code or AI tooling anywhere, never use em dashes,
commit messages are exactly one sentence, no Co-Authored-By trailers.
