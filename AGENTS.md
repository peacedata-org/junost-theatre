# Project guidance

- This is a public, independent portfolio concept inspired by the Юность cinema in Voronezh, not an official or commissioned cinema project. The repository name is historical; the venue is not a theatre.
- Keep public documentation professional, factual, and English. Visitor-facing copy may be Russian for the intended theatre audience.
- Do not copy private research, outreach drafts, credentials, personal information, or browser/session data into this repository.
- Use original, synthetic, or appropriately licensed assets; record attribution when required. Do not assume reference-site assets may be republished.
- Keep demo forms, booking, and payment flows disconnected from real services and clearly marked as demonstrations.
- Preserve responsive behavior, keyboard accessibility, reduced-motion support, and readable contrast.
- Deployment, outreach, visibility changes, and other external account changes require explicit approval for the concrete action. Git pushes to this repository's existing `origin` have standing user approval as described below.
- Do not choose a license, stack, or deployment platform without an agreed project decision.

## Local worktrees

- Keep the primary checkout on `main`; this repository is a submodule tracking `main` in the private career workspace.
- Local development worktrees live under `.worktrees/` inside the primary checkout and are ignored by Git.
- The initial design worktree is `.worktrees/design` on branch `work/design`. Implement design work there, not in the primary `main` checkout.
- Locate the primary checkout with `git worktree list` when operating from a linked worktree; do not create a second nested `.worktrees/` directory there.
- Worktrees share repository history but have separate working trees. Do not remove or overwrite another worktree's changes.
- The parent repository records a specific submodule commit even though `.gitmodules` selects `main` for remote updates. Merge approved work into `main`, then update the parent submodule pointer explicitly.

## Git push policy

- The user explicitly requests that completed commits always be pushed to the existing `origin`; do not stop at a local commit or ask for repeated push approval.
- Integrate completed, verified design work into `main` and push `main` before reporting completion. Do not merge unfinished work merely to push something.
- Before committing and pushing, check for credentials, private research, personal data, and assets without republication rights. Standing push approval is not permission to publish sensitive or unauthorized material.
- Use ordinary non-force pushes. Never overwrite remote history or discard other people's work. Report and safely resolve any push rejection.
- After pushing this repository's `main`, commit its updated submodule pointer in the private parent repository and push the parent's `main` under its own guidance.
