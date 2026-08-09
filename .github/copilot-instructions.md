# GitHub Copilot instructions for velero-io/velero

## Changelog requirement

Velero uses per-PR changelog fragments (created via `make new-changelog`) that are
assembled into release notes.  A changelog entry is **not** required when a PR
exclusively changes non-shipping content, i.e. the only files touched belong to
one or more of these categories:

| Category | Paths |
|---|---|
| GitHub Actions / CI workflows | `.github/**` |
| Documentation | `site/content/docs/**`, `site/**`, `docs/**`, `*.md` |
| Website (non-docs) | `site/**` (excluding `site/content/docs/**`) |

When you open or review a PR that falls into one of the above categories (and does
**not** modify `pkg/`, `internal/`, `cmd/`, `vendor/`, `hack/`, `go.mod`, or
`go.sum`), apply the label **`kind/changelog-not-required`** instead of requesting
a changelog entry.  The `labeler.yml` auto-labeler handles this automatically for
most cases; apply the label manually if the auto-labeler did not.

## Backport / cherry-pick workflow

Velero uses `.github/workflows/backport.yml` to automate cherry-picks onto release
branches.

- **Before merge:** comment `/backport release-1.17` (or `/cherrypick release-1.17`)
  to add the label `backport release-1.17` to the PR.  Multiple branches can be
  space-delimited: `/backport release-1.17 release-1.18`.  The label causes the
  backport to run automatically when the PR merges.
- **After merge:** the same comment immediately creates the backport PR.
- Only repository **owners, members, and collaborators** may trigger these commands.

## General coding guidelines

- Follow the existing code style of the file being edited.
- Add unit tests for new exported functions in `pkg/`.
- Do not commit secrets, credentials, or API tokens.
- Keep PRs focused; prefer small, reviewable changes over large omnibus PRs.
