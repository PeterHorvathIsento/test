# Introduction

Bluetooth mesh networking enables many-to-many (m:m) device communications and is optimized for creating large-scale device networks.

Devices may relay data to other devices not in direct radio range of the originating device. In this way, mesh networks can span very large physical areas and contain large numbers of devices. It is ideally suited for building automation, sensor networks, and other IoT solutions where tens, hundreds, or thousands of devices need to reliably and securely communicate with one another.

Bluetooth mesh is not a wireless communications technology. It's a networking technology. It uses and is dependent upon Bluetooth LE. Bluetooth LE is the wireless communications protocol stack which Bluetooth mesh makes use of.


# Specifications

The official specifications for Bluetooth mesh can be found [here](https://www.bluetooth.com/specifications/mesh-specifications)


# Getting Started with ESP BLE Mesh on ESP32

If you are new to ESP32, you may first want to go through the [getting started guide](https://docs.espressif.com/projects/esp-idf/en/latest/get-started/index.html).

ESP BLE Mesh implementation is built on top of Zephyr BLE Mesh stack. It supports network provisioning and node control as well as node features like Proxy, Relay, Low power and Friend.


## Access to ESP BLE Mesh
If you are at this page, you must have access to Espressif BLE Mesh SDK. If not, please get in touch with your point of contact to get the access.

## Documentation

The ESP BLE Mesh code in the SDK is organized as below. Each folder has corresponding source files and an included folder having header files for the functionality exposed

```
$tree components/bt/ble_mesh/

      ├── api   - BLE Mesh functionality exposed through esp_ble_mesh_* APIs for the applications
│   ├── core    - BLE Mesh Core APIs
│   │   └── include
│   └── models  - Foundation Models and other Client Models APIs
│       └── include
├── btc
│   └── include
├── mesh_core   - BLE mesh core based on Zephyr BLE stack with miscellaneous modifications
                       and an adaption layer to make it work with ESP32.
│   └── include
├── mesh_docs   - BLE Mesh docs
└── mesh_models - Foundation Models and other Client Models implementations
    └── include
```

To demonstrate the features supported by the BLE Mesh SDK we have added a few sample examples. There is a README.md file in each example for getting started. Furthermore, the examples have a walkthrough file that explains the functionality of that example in detail.

Below is a snapshot of the BLE Mesh examples directory

```
$ tree examples/bluetooth/ble_mesh/
examples/bluetooth/ble_mesh/
├── ble_mesh_client_model
│   ├── main
│   │   ├── ble_mesh_client_model_main.c
│   │   ├── board.c
│   │   ├── board.h
│   │   ├── component.mk
│   │   └── Kconfig.projbuild
│   ├── Makefile
│   ├── README.md
│   └── sdkconfig.defaults
├── ble_mesh_node
│   ├── main
│   │   ├── ble_mesh_demo_main.c
│   │   ├── board.c
│   │   ├── board.h
│   │   ├── component.mk
│   │   └── Kconfig.projbuild
│   ├── Makefile
│   ├── README.md
│   ├── sdkconfig.defaults
│   └── tutorial
│       └── Ble_Mesh_Node_Example_Walkthrough.md
└── ble_mesh_provisioner
    ├── main
    │   ├── ble_mesh_demo_main.c
    │   ├── board.c
    │   ├── board.h
    │   ├── component.mk
    │   └── Kconfig.projbuild
    ├── Makefile
    ├── README.md
    ├── sdkconfig.defaults
    └── tutorial
        └── Ble_Mesh_Provisioner_Example_Walkthrough.md

8 directories, 26 files
```


## Hardware and Setup

At present ESP32-DevKitC and ESP-WROVER-KIT are supported for BLE Mesh implementation. You can find the details about the modules [here](https://docs.espressif.com/projects/esp-idf/en/latest/hw-reference/modules-and-boards.html)

You can choose the board through menuconfig `make menuconfig -> Example Configuration -> Board selection for BLE Mesh`

Note that if you are planning to use ESP32-DevKitC, you need to connect an RGB LED to GPIO pins 25, 26 and 27.


## Sample Examples

* BLE Mesh Node

This example shows the use of BLE Mesh as a node device having a Configuration Server model and a Generic OnOff Server model. A BLE Mesh provisioner can then provision the node and control a RGB LED representing on/off state.

* BLE Mesh Client Model

This example shows how a Generic OnOff Client model within a node works. The node has a Configuration Server model, a Generic OnOff Server model and a Generic OnOff Client model.

* BLE Mesh Provisioner

This example shows how a device can act as a BLE Mesh provisioner to provision devices. The provisioner has a Configuration Server model, a Configuration Client model and a Generic OnOff Client model.


## Mobile Apps

ESP BLE Mesh implementation works with a few phone applications like Silicon Labs BLE Mesh and nRF Mesh.
These apps are available on the Google play store and iOS App Store. Additionally, we also have an in-house Android app that is still under development. You can download the apk from [here](http://download.espressif.com/BLE_MESH/BLE_Mesh_Tools/BLE_Mesh_App/EspBleMesh-v0.9.2)

Note: There is a bug in the current version of Silicon Labs App which is fixed by a workaround on the SDK side. The fix is through a configuration option (enabled by default) and needs to be disabled when using other Android/iOS apps from menuconfig `make menuconfig -> Example Configuration -> This option fixes the bug of Silicon Lab Android App 1.1.0 when reconnection will cause the sequence number to recount from 0`

## Compilation and Flashing

The first time you compile the application, you will be prompted by the menuconfig screen. You can choose the board from "Example Configuration" option. Additionally, you can modify the serial settings through "Serial flasher config option" as per your port.

BLE Mesh specific configuration options can also be modified through `make menuconfig -> Component config -> Bluetooth Mesh support`

You can still change options at any other time using "make menuconfig"
```
$ export IDF_PATH=/path/to/esp-ble-mesh-sdk-v0.x

$ cd examples/bluetooth/ble_mesh/<example_name>

$ make -j8 flash monitor
```


# Reporting Issues


* [Check the Issues section on github](https://github.com/espressif/esp-idf/issues) if you find a bug or have a feature request. Please check existing Issues and FAQs document before opening a new one.
* When you raise issues/feature requests on GitHub, please help add a tag of "BLE Mesh" into issue title, therefore we could quickly recognize and track.
