# BLE peripheral example

(See the README.md file in the upper level 'examples' directory for more information about examples.)

This example creates GATT server and then starts advertising, waiting to be connected to a GATT client.

It uses ESP32's Bluetooth controller and NimBLE stack based BLE host

This example aims at understanding GATT database configuration, advertisement and SMP related NimBLE APIs.

To test this demo, any BLE scanner app can be used.


## How to use example

### Configure the project

```
make menuconfig
```

* Set serial port under Serial Flasher Options.

* Select 'Enable NimBLE host stack' under 'Component config > Bluetooth'.

* If required, enable secure connection 4.2 from 'Component config > Bluetooth > Enable NimBLE host stack'.

* Select I/O capabilities of device from 'Example Configuration > I/O Capability', default is 'Just_works'.

* Enable/Disable other security related parameters 'Bonding, MITM option, secure connection(SM SC)' from 'Example Configuration'.

### Build and Flash

Build the project and flash it to the board, then run monitor tool to view serial output:

```
make -j4 flash monitor
```

(To exit the serial monitor, type ``Ctrl-]``.)

See the Getting Started Guide for full steps to configure and use ESP-IDF to build projects.

## Example Output

There is this console output when bleprph is connected and characteristic is read:
```
I (178) BTDM_INIT: BT controller compile version [8e87ec7]
I (178) system_api: Base MAC address is not set, read default base MAC address from BLK0 of EFUSE
I (248) phy: phy_version: 4000, b6198fa, Sep  3 2018, 15:11:06, 0, 0
I (488) NimBLE_BLE_PRPH: BLE Host Task Started
GAP procedure initiated: stop advertising.
GAP procedure initiated: advertise; disc_mode=2 adv_channel_map=0 own_addr_type=0 adv_filter_policy=0 adv_itvl_min=0 adv_itvl_max=0
connection established; status=0 handle=0 our_ota_addr_type=0 our_ota_addr=30:ae:a4:81:7c:52 our_id_addr_type=0 our_id_addr=30:ae:a4:81:7c:52 peer_ota_addr_type=1 peer_ota_addr=76:f4:04:1a:7c:96 peer_id_addr_type=1 peer_id_addr=76:f4:04:1a:7c:96 conn_itvl=36 conn_latency=0 supervision_timeout=500 encrypted=0 authenticated=0 bonded=0

connection updated; status=0 handle=0 our_ota_addr_type=0 our_ota_addr=30:ae:a4:81:7c:52 our_id_addr_type=0 our_id_addr=30:ae:a4:81:7c:52 peer_ota_addr_type=1 peer_ota_addr=76:f4:04:1a:7c:96 peer_id_addr_type=1 peer_id_addr=76:f4:04:1a:7c:96 conn_itvl=6 conn_latency=0 supervision_timeout=500 encrypted=0 authenticated=0 bonded=0

connection updated; status=0 handle=0 our_ota_addr_type=0 our_ota_addr=30:ae:a4:81:7c:52 our_id_addr_type=0 our_id_addr=30:ae:a4:81:7c:52 peer_ota_addr_type=1 peer_ota_addr=76:f4:04:1a:7c:96 peer_id_addr_type=1 peer_id_addr=76:f4:04:1a:7c:96 conn_itvl=36 conn_latency=0 supervision_timeout=500 encrypted=0 authenticated=0 bonded=0

connection updated; status=0 handle=0 our_ota_addr_type=0 our_ota_addr=30:ae:a4:81:7c:52 our_id_addr_type=0 our_id_addr=30:ae:a4:81:7c:52 peer_ota_addr_type=1 peer_ota_addr=76:f4:04:1a:7c:96 peer_id_addr_type=1 peer_id_addr=76:f4:04:1a:7c:96 conn_itvl=6 conn_latency=0 supervision_timeout=500 encrypted=0 authenticated=0 bonded=0

encryption change event; status=0 handle=0 our_ota_addr_type=0 our_ota_addr=30:ae:a4:81:7c:52 our_id_addr_type=0 our_id_addr=30:ae:a4:81:7c:52 peer_ota_addr_type=1 peer_ota_addr=76:f4:04:1a:7c:96 peer_id_addr_type=1 peer_id_addr=76:f4:04:1a:7c:96 conn_itvl=6 conn_latency=0 supervision_timeout=500 encrypted=1 authenticated=0 bonded=1

connection updated; status=0 handle=0 our_ota_addr_type=0 our_ota_addr=30:ae:a4:81:7c:52 our_id_addr_type=0 our_id_addr=30:ae:a4:81:7c:52 peer_ota_addr_type=1 peer_ota_addr=76:f4:04:1a:7c:96 peer_id_addr_type=1 peer_id_addr=76:f4:04:1a:7c:96 conn_itvl=36 conn_latency=0 supervision_timeout=500 encrypted=1 authenticated=0 bonded=1
```

## Note
* NVS support is not yet integrated to bonding. So, for now, bonding is not persistent across reboot.
