| Supported Targets | ESP32 | ESP32-C3 | ESP32-S3 |
| ----------------- | ----- | -------- | -------- |

Bluetooth Power Save Example
=================================

This example shows how to use power save mode of bluetooth.

If the modem sleep mode is enabled, bluetooth will switch periodically between active and sleep.
In sleep state, RF, PHY and BB are turned off in order to reduce power consumption.

This example contains five build configurations. For each configuration, a few configuration options are set:
- `sdkconfig.defaults.esp32_32k`: ESP32 uses 32kHz XTAL as low power clock in light sleep enabled.
- `sdkconfig.defaults.esp32c3_32k`: ESP32C3 uses 32kHz XTAL as low power clock in light sleep enabled.
- `sdkconfig.defaults.esp32c3_40m`: ESP32C3 uses main XTAL as low power clock in light sleep enabled.
- `sdkconfig.defaults.esp32s3_32k`: ESP32S3 uses 32kHz XTAL as low power clock in light sleep enabled.
- `sdkconfig.defaults.esp32s3_40m`: ESP32S3 uses main XTAL as low power clock in light sleep enabled.
## How to use example

### Hardware Required

This example should be able to run on any commonly available ESP32/ESP32-C3/ESP32-S3 development board.

### Configure the project

```
idf.py menuconfig
```

* RTC clock source can be configured in `RTC clock source > External 32kHz crystal`
* Power management can be configured in `Power Management > Support for power management`
* FreeRTOS can be configured in
    -  `FreeRTOS > (1000) Tick rate (Hz)`
    -  `FreeRTOS > Tickless idle support`
    -  `FreeRTOS > (3) Minimum number of ticks to enter sleep mode for`
* Bluetooth modem sleep can be configured in
    - `MODEM SLEEP Options > Bluetooth modem sleep`
    - `Bluetooth low power clock > External 32kHz crystal`

### Build and Flash

```
idf.py -D SDKCONFIG_DEFAULTS="sdkconfig.defaults.esp32c3_32k" set-target ESP32C3 build
```

* `-D SDKCONFIG_DEFAULTS` select configuration file to be used for creating app sdkconfig.
* `set-target ` Set the chip target to build.


To flash the project and see the output, run:


```
idf.py -p PORT flash monitor
```

(Replace PORT with the name of the serial port to use.)

(To exit the serial monitor, type ``Ctrl-]``.)

See the Getting Started Guide for full steps to configure and use ESP-IDF to build projects.

## Example Output

When you run this example, the  prints the following at the very begining:

```
I (547) BTDM_INIT: Bluetooth MAC: 7c:df:a1:66:d9:81
I (578) POWER_SAVE: REGISTER_APP_EVT, status 0, app_id 0
I (583) POWER_SAVE: CREATE_SERVICE_EVT, status 0,  service_handle 40
I (584) POWER_SAVE: REGISTER_APP_EVT, status 0, app_id 1
I (593) POWER_SAVE: SERVICE_START_EVT, status 0, service_handle 40
I (594) POWER_SAVE: ADD_CHAR_EVT, status 0,  attr_handle 42, service_handle 40
I (602) POWER_SAVE: the gatts demo char length = 3
I (608) POWER_SAVE: prf_char[0] =11
I (612) POWER_SAVE: prf_char[1] =22
I (617) POWER_SAVE: prf_char[2] =33
I (621) POWER_SAVE: CREATE_SERVICE_EVT, status 0,  service_handle 44
I (629) POWER_SAVE: ADD_DESCR_EVT, status 0, attr_handle 43, service_handle 40
I (636) POWER_SAVE: SERVICE_START_EVT, status 0, service_handle 44
I (643) POWER_SAVE: ADD_CHAR_EVT, status 0,  attr_handle 46, service_handle 44
I (652) POWER_SAVE: ADD_DESCR_EVT, status 0, attr_handle 47, service_handle 44
```

## Example Breakdown

- ESP32 does not support the use of main XTAL in light sleep mode, so an external 32kHz crystal is required.
