# NiPPE - **Ni**be **P**ower **P**erformance **E**nhancement

## Prerequisites

* [VSCode](https://code.visualstudio.com/)
* [Remote Containers Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## Open in Container

1. Clone the repository to your local machine
1. Open the repository in VSCode
1. A window will pop up in the lower left corner, asking if you want to open the repository in a container. Click "Reopen in Container"
 (**OR** press `F1` and type "Remote-Containers: Reopen in Container")

## Formatting

Formatting is strictly done by [Black](https://black.readthedocs.io/en/stable/) and the project is setup to automatically format on save.

## Versioning

Versioning follows SemVer and is handled automatically by [setuptools-git-versioning](https://setuptools-git-versioning.readthedocs.io/en/stable/) together with tags.

To get the current version you can run `setuptools-git-versioning` in a terminal inside of the repo.

## Testing

We encourage you to provide unit tests for your code contributions.

The tests should be added in the `tests/` folder and can be run by executing `pytest` in a terminal.

Tests can also be run through VSCodes [Command Palette or Test Explorer](https://code.visualstudio.com/docs/python/testing#_run-tests).

## Building code for ESP device

1. Install [ESP-IDF](https://marketplace.visualstudio.com/items?itemName=espressif.esp-idf-extension) extension in VSCode
1. Install [ESPHome](https://esphome.io/guides/installing_esphome.html#windowsii) locally
1. Change ssid and password to match your wifi in the nippegw.yaml file in the root of the project
1. Run `esphome -v compile nippegw.yaml` in the root of the project which will probably fail with the following message

    ![image](./docs/resources/compile-command-fail.png)

1. Copy the argument from the last 3 rows in the above picture i.e.

    ```bash
    --chip esp32c3 merge_bin -o C:\reps\git\nippe\.esphome\build\nippegw\.pioenvs\nippegw/firmware-factory.bin --flash_size 4MB 0x0000 C:\Users\bt6259\.platformio\packages\framework-arduinoespressif32\tools\sdk\esp32c3\bin\bootloader__40m.bin 0x8000 C:\reps\git\nippe\.esphome\build\nippegw\.pioenvs\nippegw\partitions.bin 0xe000 C:\Users\bt6259\.platformio\packages\framework-arduinoespressif32\tools\partitions\boot_app0.bin 0x10000 C:\reps\git\nippe\.esphome\build\nippegw\.pioenvs\nippegw/firmware.bin
    ```

1. Make the following change to the copied text (above = before, below = after)

    ![image](./docs/resources/merge-fix.png)

1. Run the following

    ```
    esptool.exe <Your copied text>
    ```
    in the root of the project, this will generate a binary for you to upload to the esp device.

1. Hold the "EN" button on the esp device and connect it to your computer via USB

1. Open device manager to find the COM port that the device is connected to (in our case COM9)

    ![image](./docs/resources/com-port.png)

1. Run the following command in the root of the project to flash the device

    ```
    esptool.exe --port <Your COM port> write_flash --flash_mode dio --flash_freq 80m --flash_size 4MB 0x0 .\.esphome\build\nippegw\.pioenvs\nippegw\firmware-factory.bin
    ```

1. Press the "BOOT" button on the esp device to load the new firmware, the device will show up as a wifi called "nippegw" in your wifi list