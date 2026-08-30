# RPM Packages

Public directory and migration home for the Reaper RPM repository network.

## Target architecture

Binary publication is being split into six physically independent public repositories:

- `johngrimmreaper/rhel9-rpms`
- `johngrimmreaper/rhel9-testing-rpms`
- `johngrimmreaper/rhel10-rpms`
- `johngrimmreaper/rhel10-testing-rpms`
- `johngrimmreaper/fedora44-rpms`
- `johngrimmreaper/fedora44-testing-rpms`

Each is paired with one private `*-rpm-packaging` control repository. The public repositories contain generated consumer-safe state only; package YAML, source pins, build policy, and private operational configuration remain in the paired private controller.

The new public repositories intentionally start fresh. Existing RPM binaries in the legacy combined deployment do not need to be migrated; packages can be rebuilt from the migrated controller profiles.

## Portal role

After the split is proven, `https://johngrimmreaper.github.io/rpm-packages/` becomes the top-level directory linking all six channel sites. The polished portal is staged on `main` during migration.

The existing `gh-pages` deployment remains intact until the new repositories and their first generated snapshots exist, avoiding a transition window where the public directory points only to unavailable sites.

## Generated publication policy

Each public binary repository uses the same `rpm-builder` generated repository browser and publication model:

1. start from the current channel snapshot when one exists;
2. replace superseded package names for the affected target;
3. add the new signed RPMs;
4. regenerate `createrepo_c` metadata;
5. sign repository metadata when enabled;
6. regenerate package browsing, install instructions, repository statistics, storage usage, and the latest-package preview;
7. validate the complete staged repository in a fresh Mock environment;
8. create a commit with no parents;
9. update only the dedicated Pages deployment branch with a lease guard.

This keeps ordinary binary history from accumulating as reachable Git history and makes each public repository independently rebuildable and independently bounded.
