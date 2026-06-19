> For firmware version 0.x.x

Board config file is named _board.cfg_ is stored on _cfg_ partition. 
During flashing there is option _BOARD_CONFIG_DEPLOY_ for deploy config and option _BOARD_CONFIG_ say which config will be deployed.
This is required only first time, or after changing configuratrion.
All board configs are stored in [_cfg_](https://github.com/dzurikmiroslav/esp32-evse/tree/master/cfg) directory.

![Board config](https://github.com/dzurikmiroslav/esp32-evse/wiki/images/board-config-deploy.png "Board config")

## File format

| Key                             | Description                                   | Representation           |
| ------------------------------- | --------------------------------------------- | ------------------------ |
| DEVICE_NAME                     | Name of the device                            | char[32]                 |
| LED_CHARGING                    | Has charging led                              | bool                     |
| LED_CHARGING_GPIO               | Charging led gpio                             | uint32                   |
| LED_ERROR                       | Has error led                                 | bool                     |
| LED_ERROR_GPIO                  | Error led gpio                                | uint32                   |
| LED_WIFI                        | Has WiFi connection led                       | bool                     |
| LED_WIFI_GPIO                   | WiFi connection led gpio                      | uint32                   |
| BUTTION_WIFI_GPIO               | WiFi button gpio                              | uint32                   |
| PILOT_PWM_GPIO                  | CP pwm generator gpio                         | uint32                   |
| PILOT_ADC_CHANNEL               | CP sensing adc channel                        | uint32                   |
| PILOT_DOWN_THRESHOLD_12         | A state high voltage down threshold in mV     | uint16                   |
| PILOT_DOWN_THRESHOLD_9          | B state high voltage down threshold in mV     | uint16                   |
| PILOT_DOWN_THRESHOLD_6          | C state high voltage down threshold in mV     | uint16                   |
| PILOT_DOWN_THRESHOLD_3          | D state high voltage down threshold in mV     | uint16                   |
| PILOT_DOWN_THRESHOLD_N12        | B,C,D state low voltage threshold in mV       | uint16                   |
| PROXIMITY                       | Has PP detection                              | bool                     |
| PROXIMITY_ADC_CHANNEL           | PP sensing adc channel                        | uint32                   |
| PROXIMITY_DOWN_THRESHOLD_13     | Cable 13A down threshold                      | uint16                   |
| PROXIMITY_DOWN_THRESHOLD_20     | Cable 20A down threshold                      | uint16                   |
| PROXIMITY_DOWN_THRESHOLD_32     | Cable 32A down threshold                      | uint16                   |
| AC_RELAY_GPIO                   | AC relay gpio for controlling mains contactor | uint32                   |
| SOCKET_LOCK                     | Has socket lock                               | bool                     |
| SOCKET_LOCK_A_GPIO              |                                               | uint32                   |
| SOCKET_LOCK_B_GPIO              |                                               | uint32                   |
| SOCKET_LOCK_DETECTION_GPIO      |                                               | uint32                   |
| SOCKET_LOCK_DETECTION_DELAY     |                                               | uint16                   |
| SOCKET_LOCK_MIN_BREAK_TIME      |                                               | uint16                   |
| RCM                             | Has residual current monitor                  | bool                     |
| RCM_GPIO                        | Residual current monitor gpio                 | uint32                   |
| RCM_TEST_GPIO                   | Resudal current monitor test gpio             | uint32                   |
| ENERGY_METER                    | Energy meter                                  | enum(none, cur, cur_vlt) |
| ENERGY_METER_THREE_PHASES       |                                               | bool                     |
| ENERGY_METER_L1_CUR_ADC_CHANNEL |                                               | uint32                   |
| ENERGY_METER_L2_CUR_ADC_CHANNEL |                                               | uint32                   |
| ENERGY_METER_L3_CUR_ADC_CHANNEL |                                               | uint32                   |
| ENERGY_METER_CUR_SCALE          |                                               | float                    |
| ENERGY_METER_L1_VLT_ADC_CHANNEL |                                               | uint32                   |
| ENERGY_METER_L2_VLT_ADC_CHANNEL |                                               | uint32                   |
| ENERGY_METER_L3_VLT_ADC_CHANNEL |                                               | uint32                   |
| ENERGY_METER_VLT_SCALE          |                                               | float                    |
| AUX_IN_1                        | Has digital input 1                           | bool                     |
| AUX_IN_1_NAME                   | Digital input 1 name                          | char[8]                  |
| AUX_IN_1_GPIO                   | Digital input 1 gpio                          | uint32                   |
| AUX_IN_2                        | Has digital input 2                           | bool                     |
| AUX_IN_2_NAME                   | Digital input 2 name                          | char[8]                  |
| AUX_IN_2_GPIO                   | Digital input 2 gpio                          | uint32                   |
| AUX_IN_3                        | Has digital input 3                           | bool                     |
| AUX_IN_3_NAME                   | Digital input 3 name                          | char[8]                  |
| AUX_IN_3_GPIO                   | Digital input 3 gpio                          | uint32                   |
| AUX_IN_4                        | Has digital input 4                           | bool                     |
| AUX_IN_4_NAME                   | Digital input 4 name                          | char[8]                  |
| AUX_IN_4_GPIO                   | Digital input 4 gpio                          | uint32                   |
| AUX_OUT_1                       | Has digital output 1                          | bool                     |
| AUX_OUT_1_NAME                  | Digital output 1 name                         | char[8]                  |
| AUX_OUT_1_GPIO                  | Digital output 1 gpio                         | uint32                   |
| AUX_OUT_2                       | Has digital output 2                          | bool                     |
| AUX_OUT_2_NAME                  | Digital output 2 name                         | char[8]                  |
| AUX_OUT_2_GPIO                  | Digital output 2 gpio                         | uint32                   |
| AUX_OUT_3                       | Has digital output 3                          | bool                     |
| AUX_OUT_3_NAME                  | Digital output 3 name                         | char[8]                  |
| AUX_OUT_3_GPIO                  | Digital output 3 gpio                         | uint32                   |
| AUX_OUT_4                       | Has digital output 4                          | bool                     |
| AUX_OUT_4_NAME                  | Digital output 4 name                         | char[8]                  |
| AUX_OUT_4_GPIO                  | Digital output 4 gpio                         | uint32                   |
| AUX_AIN_1                       | Has analog input 1                            | bool                     |
| AUX_AIN_1_NAME                  | Analog input 1 name                           | bool                     |
| AUX_AIN_1_ADC_CHANNEL           | Analog input 1 adc channel                    | uint32                   |
| AUX_AIN_2                       | Has analog input 2                            | bool                     |
| AUX_AIN_2_NAME                  | Analog input 2 name                           | bool                     |
| AUX_AIN_2_ADC_CHANNEL           | Analog input 2 adc channel                    | uint32                   |
| SERIAL_1                        | Type of serial                                | enum(none, uart, rs485)  |
| SERIAL_1_NAME                   | Name of serial                                | char[16]                 |
| SERIAL_1_RXD_GPIO               | Serial rx gpio                                | uint32                   |
| SERIAL_1_TXD_GPIO               | Serial tx gpio                                | uint32                   |
| SERIAL_1_RTS_GPIO               | Serial rts gpio                               | uint32                   |
| SERIAL_2                        | Type of serial                                | enum(none, uart, rs485)  |
| SERIAL_2_NAME                   | Name of serial                                | char[16]                 |
| SERIAL_2_RXD_GPIO               | Serial rx gpio                                | uint32                   |
| SERIAL_2_TXD_GPIO               | Serial tx gpio                                | uint32                   |
| SERIAL_2_RTS_GPIO               | Serial rts gpio                               | uint32                   |
| SERIAL_3 *                      | Type of serial                                | enum(none, uart, rs485)  |
| SERIAL_3_NAME *                 | Name of serial                                | char[16]                 |
| SERIAL_3_RXD_GPIO *             | Serial rx gpio                                | uint32                   |
| SERIAL_3_TXD_GPIO *             | Serial tx gpio                                | uint32                   |
| SERIAL_3_RTS_GPIO *             | Serial rts gpio                               | uint32                   |
| ONEWIRE                         | Has onewire bus                               | bool                     |


**Note** Serial 3 is available only on MCU that have more than two uarts.