# NiPPE - **Ni**be **P**ower **P**erformance **E**nhancement

[![Lint](https://github.com/Wesztman/nippe/actions/workflows/lint.yaml/badge.svg)](https://github.com/Wesztman/nippe/actions/workflows/lint.yaml)
[![Builder](https://github.com/Wesztman/nippe/actions/workflows/builder.yaml/badge.svg)](https://github.com/Wesztman/nippe/actions/workflows/builder.yaml)
[![Container](https://ghcr-badge.herokuapp.com/wesztman/nippe/latest_tag)](https://github.com/Wesztman/nippe/pkgs/container/nippe)
## Contributing
### Prerequisites

* [VSCode](https://code.visualstudio.com/)
* [Remote Containers Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### Open in Container

1. Clone the repository to your local machine
2. Open the repository in VSCode
3. A window will pop up in the lower left corner, asking if you want to open the repository in a container. Click "Reopen in Container"
 (**OR** press `F1` and type "Remote-Containers: Reopen in Container")

### Testing addon locally

1. Press `F1` and type "Run Task"
2. Choose "Start Home Assistant"
3. Wait for the container to start, this can take a while
4. You can now access Home Assistant at [http://localhost:7123](http://localhost:7123)
5. The addons in the repository are now available in the "Add-on Store" under local addons in Home Assistant

### Documentation

https://developers.home-assistant.io/docs/add-ons