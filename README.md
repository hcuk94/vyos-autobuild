# vyos-autobuild

![VyOS Autobuild Robot Workflow Status](https://github.com/hcuk94/vyos-autobuild/actions/workflows/main.yml/badge.svg)

Automation-only repo which uses GitHub Actions to build the latest stable release of VyOS each time a new version is released to the official VyOS repo.

It works as follows:
1. Automation runs on schedule and clones the vyos/vyos-build repo, checking for the most recent tagged release. 
2. If the latest version tag is different to the one recorded in this repo's release.txt file, the newer version will be built.
3. The official VyOS docker container is used for the build, with the resulting .iso file uploaded to a tagged release in this repo.
4. Upon successful build, the release.txt file in this repo is updated so that we don't rebuild until another release is published by VyOS.

## Limitations
- The builds are completely untested at the point of release.
- The automation may break if VyOS change how they name parts of their official build repo. If that happens I will endeavour to update this repo.
- Manual mappings are required from version numbers to branch names (i.e. 1.3.x = equuleum). This is because while VyOS tag LTS version numbers in their GitHub repo, they advise building from the latest branch commits and Docker image, which will still provide the stable/LTS version, but with latest bugfixes etc included.

Pull requests are welcome!