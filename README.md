# RPM Packages

Public deployment repository for signed Fedora and Red Hat Enterprise Linux RPM repositories.

## Branch policy

`main` contains only documentation and lightweight repository information.

`gh-pages` is generated deployment state served by GitHub Pages. It is intentionally not an archival package-history branch. Every real publication replaces it with a new parentless snapshot commit after repository validation.

The publication process:

1. starts from the currently published file snapshot
2. removes superseded package names for the affected target
3. adds the new signed RPMs
4. regenerates `createrepo_c` metadata
5. signs repository metadata when enabled
6. validates the complete staged target in a fresh Mock environment
7. creates a commit with no parents
8. force-updates only `gh-pages`

This keeps obsolete binary packages out of reachable Git history and minimizes GitHub storage growth.

The build engine and package configuration histories live separately in private repositories; generated build artifacts do not belong on `main`.
