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
1. Open the repository in VSCode
1. A window will pop up in the lower left corner, asking if you want to open the repository in a container. Click "Reopen in Container"
 (**OR** press `F1` and type "Remote-Containers: Reopen in Container")

### Testing addon locally

1. Press `F1` and type "Run Task"
1. Choose "Start Home Assistant"
1. Wait for the container to start, this can take a while
1. You can now access Home Assistant at [http://localhost:7123](http://localhost:7123)
1. The addons in the repository are now available in the "Add-on Store" under local addons in Home Assistant

### Documentation

<https://developers.home-assistant.io/docs/add-ons>

### Building code for ESP device

1. Install [ESP-IDF](https://marketplace.visualstudio.com/items?itemName=espressif.esp-idf-extension) extension in VSCode
1. Install [ESPHome](https://esphome.io/guides/installing_esphome.html#windowsii) locally
1. Change ssid and password to match your wifi in the nippegw.yaml file in the root of the project
1. Run `esphome -v compile nippegw.yaml` in the root of the project which will probably fail with the following message

    ![image](.\doc\resources\compile-command-fail.png)

1. Copy the argument from the last 3 rows in the above picture i.e.

    ```bash
    --chip esp32c3 merge_bin -o C:\reps\git\nippe\.esphome\build\nippegw\.pioenvs\nippegw/firmware-factory.bin --flash_size 4MB 0x0000 C:\Users\bt6259\.platformio\packages\framework-arduinoespressif32\tools\sdk\esp32c3\bin\bootloader__40m.bin 0x8000 C:\reps\git\nippe\.esphome\build\nippegw\.pioenvs\nippegw\partitions.bin 0xe000 C:\Users\bt6259\.platformio\packages\framework-arduinoespressif32\tools\partitions\boot_app0.bin 0x10000 C:\reps\git\nippe\.esphome\build\nippegw\.pioenvs\nippegw/firmware.bin
    ```

1. Make the following change to the copied text (above = before, below = after)

    ![image](.\doc\resources\merge-fix.png)

1. Run the following

    ```
    esptool.exe <Your copied text>
    ```
    in the root of the project, this will generate a binary for you to upload to the esp device.

1. Hold the "EN" button on the esp device and connect it to your computer via USB

1. Open device manager to find the COM port that the device is connected to (in our case COM9)

    ![image](.\doc\resources\com-port.png)

1. Run the following command in the root of the project to flash the device

    ```
    esptool.exe --port <Your COM port> write_flash --flash_mode dio --flash_freq 80m --flash_size 4MB 0x0 .\.esphome\build\nippegw\.pioenvs\nippegw\firmware-factory.bin
    ```

1. Press the "BOOT" button on the esp device to load the new firmware, the device will show up as a wifi called "nippegw" in your wifi list