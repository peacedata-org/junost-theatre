# Project guidance

- This is a public, independent portfolio concept, not an official or commissioned theatre project.
- Keep public documentation professional, factual, and English. Visitor-facing copy may be Russian for the intended theatre audience.
- Do not copy private research, outreach drafts, credentials, personal information, or browser/session data into this repository.
- Use original, synthetic, or appropriately licensed assets; record attribution when required. Do not assume reference-site assets may be republished.
- Keep demo forms, booking, and payment flows disconnected from real services and clearly marked as demonstrations.
- Preserve responsive behavior, keyboard accessibility, reduced-motion support, and readable contrast.
- Publication, deployment, outreach, and changes to external accounts require explicit approval for the concrete action.
- Do not choose a license, stack, or deployment platform without an agreed project decision.

## Local worktrees

- Keep the primary checkout on `main`; this repository is a submodule tracking `main` in the private career workspace.
- Local development worktrees live under `.worktrees/` inside the primary checkout and are ignored by Git.
- The initial design worktree is `.worktrees/design` on branch `work/design`. Implement design work there, not in the primary `main` checkout.
- Locate the primary checkout with `git worktree list` when operating from a linked worktree; do not create a second nested `.worktrees/` directory there.
- Worktrees share repository history but have separate working trees. Do not remove or overwrite another worktree's changes.
- The parent repository records a specific submodule commit even though `.gitmodules` selects `main` for remote updates. Merge approved work into `main`, then update the parent submodule pointer explicitly.
