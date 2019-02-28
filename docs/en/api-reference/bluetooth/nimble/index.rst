NimBLE-based host APIs
**********************
Overview
========

NimBLE is a highly configurable and BT SIG qualifiable BLE stack providing both host and controller functionalities. ESP-IDF now supports a version of NimBLE host stack which is specifically ported for ESP platform and FreeRTOS. The underlying controller is still the same (as in case of Bluedroid) providing VHCI interface. Refer to  `NimBLE user guide <http://mynewt.apache.org/latest/network/docs/index.html#>`_ for complete list of features and additional information on NimBLE stack. Most features of NimBLE including BLE Mesh are supported by ESP-IDF. The porting is performed with the intention of keeping nimBLE APIs intact from application perspective.

Architecture
============

Currently, NimBLE host and controller support different transports such UART and RAM between them. However, RAM transport cannot be used as is in case of ESP as ESP controller supports VHCI interface and buffering schemes used by NimBLE host is incompatible with that used by ESP controller. Therefore, a new transport between NimBLE host and ESP controller has been added. This is depicted in the figure below. This layer is responsible for maintaining pool of transport buffers and formatting buffers exchanges between host and controller as per the requirements.

.. figure:: ../../../../_static/esp32_nimble_stack.png
    :align: center
    :alt: ESP NimBLE Stack.
    :scale: 50

    ESP NimBLE Stack


Threading Model
===============

The NimBLE host can run inside the application thread or can have its own independent thread. This flexibility is inherently provided by NimBLE design. By default, a thread is spawned by the porting function ``nimble_port_freertos_init``. This behavior can be changed by overriding the same function. For BLE Mesh, additional thread (advertising thread) is used which keeps on feeding advertisement events to the main thread.

Programming Sequence
====================

Typical programming sequence with NimBLE stack consists of the following steps:
    * Initialize NVS flash using ``nvs_flash_init`` API. This is because ESP controller uses NVS during initialization.
    * Call ``esp_nimble_hci_and_controller_init`` to initialise ESP controller as well as transport layer. This will also link the host and controller modules together. Alternatively, if ESP controller is already initialized, then ``esp_nimble_hci_init`` can be called to the remaining initialization.
    * Initialize the host stack using ``nimble_port_init``.
    * Initialize services using corresponding init APIs (For example, ``ble_svc_gap_init``, ``ble_svc_gatt_init``, ``ble_svc_ans_init`` and so on).
    * Run the thread for host stack using ``nimble_port_freertos_init``

This documentation does not cover NimBLE APIs. Refer to `NimBLE tutorial <https://mynewt.apache.org/latest/network/docs/index.html#ble-user-guide>`_ for more details on the programming sequence/NimBLE APIs for different scenarios.

API Reference
=============

.. include:: /_build/inc/esp_nimble_hci.inc
