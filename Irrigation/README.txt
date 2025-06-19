REPLACING THE MICROPROCESSOR IN THE RAIN SOAKED BEEHYVE
1. Used a nanoMCP that was laying around to first blink some LEDs using led-test.yaml then put a jumper from one of the LEDs to the Triac on the busted BEEHYVE - worked
	- cd to d:\Users\dstac\HardwareProjects\Irrigation
	- esphome compile led-test.yaml (this took quite a while!)
	- results was found in D:\Users\dstac\HardwareProjects\Irrigation\.esphome\build\led-test\.pioenvs\led-test and is firmware.bin
	- Plug in the MCP and enter: esphome upload led-test.yaml --device COM3
	- esphome logs led-test.yaml


6/19/25
- flashed and wired power to the D1.  Have not added it to HA or wired in LEDs




led-test.yaml code is below:

esphome:
  name: led-test
  friendly_name: LED Test

esp8266:
  board: d1_mini

# Enable logging
logger:

# Enable Home Assistant API
api:

# Over-the-Air updates (platform now required)
ota:
  platform: esphome

wifi:
  ssid: "Stack52-5G"
  password: "ReallyFastStack"

#  manual_ip:
#     static_ip: 192.168.0.212
#     gateway: 192.168.0.1
#     subnet: 255.255.255.0

  ap:
    ssid: "led-test Fallback Hotspot"
    password: "fallback123"

captive_portal:

output:
  - platform: gpio
    pin: D2  # mislabeled, actually GPIO4
    id: led1
  - platform: gpio
    pin: D1  # mislabeled, actually GPIO5
    id: led2

light:
  - platform: binary
    name: "LED 1"
    output: led1
  - platform: binary
    name: "LED 2"
    output: led2