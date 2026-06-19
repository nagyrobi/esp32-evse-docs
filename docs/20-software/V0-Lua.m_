> For firmware version 0.x.x

Script capability allows custom functionality of controller, is based on [Lua](https://lua.org/).

Script settings are in web interface, when you can enable/disable this feature and browsing print output. 
In Files web interface, you can edit Lua sources. At startup file `/data/init.lua` will be executed.
Lua sources also can be edited through WebDAV, just open in file browser url: `dav://<IP>/dav/data/`. I recommended this way, because you can use favorite Lua IDE...

In addition to the standard Lua functionality, there is additional modules for controlling charging controller:
* [`evse`](#evse-module)
* [`boardconfig`](#boardconfig-module)
* [`aux`](#aux-module)
* [`mqtt`](#mqtt-module)
* [`json`](#json-module)

## `evse` module

Root level module, for controlling charging controller. Globally loaded, not need require this module.

| Constant                    | Description              |
| --------------------------- | ------------------------ |
| evse.STATEA                 | State A                  |
| evse.STATEB1                | State B1                 |
| evse.STATEB2                | State B2                 |
| evse.STATEC1                | State C1                 |
| evse.STATEC2                | State C2                 |
| evse.STATED1                | State D1                 |
| evse.STATED2                | State D2                 |
| evse.STATEE                 | State E                  |
| evse.STATEF                 | State F                  |
| evse.ERRPILOTFAULTBIT       | Error pilot_fault        |
| evse.ERRDIODESHORTBIT       | Error diode_short        |
| evse.ERRLOCKFAULTBIT        | Error lock_fault         |
| evse.ERRUNLOCKFAULTBIT      | Error unlock_fault       |
| evse.ERRRCMTRIGGEREDBIT     | Error rcm_triggered      |
| evse.ERRRCMSELFTESTFAULTBIT | Error rcm_selftest_fault |
| evse.ERRTEMPERATUREHIGHBIT  | Error temperature_high   |
| evse.ERRTEMPERATUREFAULTBIT | Error temperature_fault  |

| Function                | Signature                 | Description                                        |
| ----------------------- | ------------------------- | -------------------------------------------------- |
| evse.getstate           | `():number`               | Get state, possible values `evse.STATE...`         |
| evse.geterror           | `():number`               | Get error bits, possible values `evse.ERR...` bits |
| evse.getenabled         | `():boolean`              | Get charging enabled                               |
| evse.setenabled         | `(boolean):nil`           | Set charging enabled                               |
| evse.getavailable       | `():boolean`              | Get controller available                           |
| evse.setavailable       | `(boolean):nil`           | Set controller available                           |
| evse.getchargingcurrent | `():number`               | Get charging current in A*10                       |
| evse.setchargingcurrent | `(number):nil`            | Set charging current in A*10                       |
| evse.getpower           | `():number`               | Get charging power in W                            |
| evse.getchargingtime    | `():number`               | Get charging time in s                             |
| evse.getsessiontime     | `():number`               | Get session time in s                              |
| evse.getconsumption     | `():number`               | Get consumption in Wh                              |
| evse.getvoltage         | `():number,number,number` | Get voltages in V                                  |
| evse.getcurrent         | `():number,number,number` | Get current in A                                   |
| evse.getlowtemperature  | `():number`               | Get low temperature                                |
| evse.gethightemperature | `():number`               | Get high temperature                               |
| evse.adddriver          | `(table):nil`             | Add driver                                         |

### Driver
Driver is table instance which has predefined event methods:
* `loop`: called every script task loop, approx 50ms
* `every100ms`: called every 100ms
* `every250ms`: called every 250ms
* `every1s`: called every second

Example:
```lua
local mydriver = {
  every1s = function()
    evse.setenabled(aux.read("IN1"))
  end
}

evse.adddriver(mydriver)
```

## `boardconfig` module
This module providing values from `board.cfg`. Not globally loaded, need require this module.

| Constant                      | Description                      |
| ----------------------------- | -------------------------------- |
| boardconfig.ENERGYMETERNONE   | Energy meter none                |
| boardconfig.ENERGYMETERCUR    | Energy meter current             |
| boardconfig.ENERGYMETERCURVLT | Energy meter current and voltage |
| boardconfig.SERIALNONE        | Serial none                      |
| boardconfig.SERIALUART        | Serial UART                      |
| boardconfig.SERIALRS485       | Serial RS485                     |

| Value                              | Description                                                      |
| ---------------------------------- | ---------------------------------------------------------------- |
| boardconfig.devicename             | Name of the device (string)                                      |
| boardconfig.proximity              | Has PP detection (bool)                                          |
| boardconfig.socketlock             | Has socket lock (bool)                                           |
| boardconfig.rcm                    | Has residual current monitor (bool)                              |
| boardconfig.energymeter            | Energy meter (int), possible values `boardconfig.ENERGYMETER...` |
| boardconfig.energymeterthreephases | Is energy meter three phases (bool)                              |
| boardconfig.serial1                | Type of serial 1 (int), possible values `boardconfig.SERIAL...`  |
| boardconfig.serial2                | Type of serial 2 (int), possible values `boardconfig.SERIAL...`  |
| boardconfig.serial3                | Type of serial 3 (int), possible values `boardconfig.SERIAL...`  |
| boardconfig.onewire                | Has onewire bus (bool)                                           |
| boardconfig.onewiretempsensor      | Has temperature sensor on onewire (bool)                         |
| boardconfig.auxin                  | AUX digital input names (string array)                           |
| boardconfig.auxout                 | AUX digital output names (string array)                          |
| boardconfig.auxain                 | AUX analog input names (string array)                            |

Example:
```lua
local boardconfig = require("boardconfig")

print("device name:", boardconfig.devicename)
```

## `aux` module
This module providing access to AUX. Not globally loaded, need require this module.

| Function       | Signature          | Description              |
| -------------- | ------------------ | ------------------------ |
| aux.write      | `(string):boolean` | Set digital output value |
| aux.read       | `(string):boolean` | Get digital input value  |
| aux.analogread | `(string):number`  | Get analog input value   |

## `mqtt` module
This module providing access to MQTT broker. Not globally loaded, need require this module.

| Function                 | Signature                                                                      | Description                |
| ------------------------ | ------------------------------------------------------------------------------ | -------------------------- |
| mqtt.client              | `(uri: string [, user: string] [, password: string]]):table`                   | Create mqtt client         |
| mqtt.client:setonconnect | `(function):nil`                                                               | Set on connect handler     |
| mqtt.client:setonmessage | `(function):nil`                                                               | Set on message handler     |
| mqtt.client:connect      | `():nil`                                                                       | Connects to the broker     |
| mqtt.client:disconnect   | `():nil`                                                                       | Disconnect from the broker |
| mqtt.client:subscribe    | `(topic: string [, qos: number = 1]):nil`                                      | Subscribe to topic         |
| mqtt.client:unsubscribe  | `(topic: string):nil`                                                          | Unsubscribe from topic     |
| mqtt.client:publish      | `(topic: string, data: string [, qos: number = 1] [, retry: number = 0]]):nil` | Publish message            |

Example:
```lua
local mqtt = require("mqtt")

local client = mqtt.client("mqtt://broker.hivemq.com:1883")

client:setonconnect(function()
 client:publish("test/message", "Connected!")
end)

client:connect()
```

## `json` module
This module JSON serialization & deserialization. Not globally loaded, need require this module.

| Function    | Signature                                                           | Description                   |
| ----------- | ------------------------------------------------------------------- | ----------------------------- |
| json.encode | `(table\|number\|boolean\|string\|nil[, formated: boolean]):string` | Encode Lua value to JSON      |
| json.decode | `(string):table\|number\|boolean\|string\|nil`                      | Decode from JSON to Lua value |

Example:
```lua
local json = require("json")

local value = {
  num = 123,
  str = "abc",
  logical = true
}
print(json.encode(value, true))
```

## Complex example
Here is example with two drivers, first handling emergency stop button, second sending telemetry data to thingsboard cloud.
For better code readability, each driver is in its own script file, the main script `init.lua` imports them.

File `/data/init.lua`:
```lua
evse.adddriver(require("emstop"))
evse.adddriver(require("tb"))
```

Fili `/data/emstop.lua`:
```lua
local aux = require("aux")

return {
  every1s = function ()
    local emstop = aux.read("IN2")
    if not emstop ~= evse.getavailable() then
      evse.setavailable(not emstop)
    end
  end
}
```

File `/data/tb.lua`:
```lua
local mqtt = require("mqtt")
local json = require("json")

local client = mqtt.client("mqtt://demo.thingsboard.io:1883", "your password")

client:setonconnect(function()
  print("tb contected")
end)

client:connect()

function send()
  local payload = {}
  local state = evse.getstate()
  payload["session"] = (state >= evse.STATEB1 and state <= evse.STATED2) and 1 or 0
  payload["charging"] = (state == evse.STATE_C2 or state == evse.STATE_D2) and 1 or 0
  payload["enabled"] = evse.getenabled() and 1 or 0
  payload["power"]  = evse.getpower()
  payload["consumption"] = evse.getconsumption()
  payload["voltageL1"], payload["voltageL2"], payload["voltageL3"] = evse.getvoltage()
  payload["currentL1"], payload["currentL2"], payload["currentL3"] = evse.getcurrent()
  payload["temperature"] = evse.gethightemperature()
  payload["uptime"] = os.clock()

  client:publish("v1/devices/me/telemetry", json.encode(payload))
end

local counter = 0

return {
  every1s = function ()
    if counter == 60 then
      send()
      counter = 0
    end
    counter = counter + 1
  end
}

```
