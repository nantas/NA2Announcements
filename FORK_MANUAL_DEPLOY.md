# nantas/NA2Announcements (Fork)

This fork is a **manual-deploy testing ground** for announcement content before
promoting to the upstream `VeewoGames/NA2Announcements` repository.

## Purpose

- Stage and preview new/edited announcement content locally
- Validate formatting (markdown, index.json structure, image references)
- Manually deploy to the dev environment for end-to-end verification

## No Auto-Deploy Here

Automated CloudBase deployment (dev + prod) lives **only** in the upstream
[`VeewoGames/NA2Announcements`](https://github.com/VeewoGames/NA2Announcements)
repository. Pushing to this fork's `master` does **not** trigger any deployment.

This workflow file was intentionally removed in commit `40162d6e`. Do not
re-add an auto-deploy workflow here — it would duplicate the upstream pipeline
and risk double-deploying / divergent state.

## Manual Deploy (Dev Only)

To manually deploy this fork's content to the **dev** environment for testing:

```bash
# From the repo root, using tcb CLI (requires local CloudBase login)
tcb hosting deploy ./ / -e neon-backend-dev-3fx27og6365fcc6 --json
```

Remember to `rm -rf .git` before deploy, or copy content to a clean directory,
since `tcb hosting deploy` traverses the working directory and `.git` may
trigger permission errors.

## Promoting to Production

Once content is validated in dev, open a PR from this fork to
`VeewoGames/NA2Announcements`. Merging the PR triggers the upstream
auto-deploy workflow, which deploys to both dev and prod simultaneously.
