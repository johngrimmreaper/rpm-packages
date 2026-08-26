# Repository policy

This repository is a deployment target, not a binary archive.

## `main`

Keep `main` small. It may contain documentation, public keys, or lightweight client configuration, but it must not accumulate generated RPM build history.

## `gh-pages`

`gh-pages` is disposable generated state and is served by GitHub Pages.

Publication must use a parentless snapshot commit. Normal incremental publication commits are forbidden once RPM content is managed by the builder.

The builder must refuse destructive snapshot publication when the target branch is `main` or the repository default branch.

Superseded RPMs are removed by RPM package name, repository metadata is regenerated from the final staged package set, and the staged repository is validated before the branch is force-updated.

Old unreachable Git objects may remain on GitHub until server-side garbage collection; keeping every deployment parentless prevents them from remaining part of reachable history.
