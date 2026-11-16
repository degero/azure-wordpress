# Maintaining azure-wordpress

Notes for maintainers on release and dependency workflows. This complements [CONTRIBUTING.md](./CONTRIBUTING.md), which covers the general contribution process for everyone.

## Builds and Docker pushes

Github workflows will push PR builds of the docker image with a version pr-#. Main branch will build but not push. Any tags are built and pushed. For testing out before cutting a release see below about doing a Release Candidate version.

## Versioning

This is handled via git tags of `vX.X.X` and docker images set with this version. Tags are created automatically by release-please based on the conventions noted in [CONTRIBUTING.md](CONTRIBUTING.md#pull-request-title)

## Release process

Once 'main' has your PRs merged. To initiate a new release (eg below with v2.3.0):

1. Determine the new version number based on either the active release-please PR tag name or determine it from the [conventions](CONTRIBUTING.md#pull-request-title)
1. Tag a -rc.# of latest main for the new version eg `git tag v2.3.0-rc.1`
1. Push this tag `git push origin v2.3.0-rc.1`
1. The `release.yml` workflow will build and push an docker image `chaddotnet/azure-wordpress:v2.3.0-rc.1`
1. Confirm everything for the version is correct by using that docker image vesion
1. Notify maintainers to test the new rc
1. If there are any issues initiate fixes and follow the prior steps again with an incremented rc eg `v2.3.0-rc.2`
1. Find the open **release-please PR** (it auto-opens/updates on every push to `main` with a "release: x.y.z" title). If it's not open, check the `release-please` workflow ran on your latest merge to `main`.
1. Review the PR diff — confirm `CHANGELOG.md` and `.release-please-manifest.json` look right (correct version bump, all expected entries present).
1. **Merge the release-please PR**
1. On merge, release-please:
   - Bumps `.release-please-manifest.json` to the new version.
   - Creates the git tag eg `v2.3.0` (final, no `-rc` suffix) and a GitHub Release.
1. The pushed `v2.3.0` tag triggers `Release.yml` and:
   - Builds and pushes the release docker image to dockerhub.
   - Sends notification on release failure
1. Verify the release:
   - Check `https://hub.docker.com/repository/docker/chaddotnet/azure-wordpress/tags` shows the version released.
   - Check the [releases](https://github.com/degero/azure-wordpress/releases) notes match [CHANGELOG.md](./CHANGELOG.md).
