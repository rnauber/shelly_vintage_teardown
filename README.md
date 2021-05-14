# Teardown of a Shelly Vintage Bulb


<img src="https://user-images.githubusercontent.com/7414650/118321306-b61cd300-b4fd-11eb-918d-ff4da7fe3690.jpg" height="400" >

## Backstory

Well I got myself an [Shelly Vintage Light Bulb](https://shelly.cloud/products/shelly-vintage-smart-home-automation-bulb/) to flash it with a custom <a href="https://esphome.io/"><img src="https://esphome.io/_images/logo-text.png" height="16" ></a> firmware. This worked flawlessy following [this tutorial](https://savjee.be/2020/09/shelly-2.5-flash-esphome-over-the-air/). Unfortunately, after flashing several custom firmwares, I got a little to fancy and bricked the device 😭.
There are no accessible electrical interfaces on that bulb except for the mains voltage. Furthermore, I failed to trigger the safe mode of ESPhome
by powercycling it 10 times...

## Landfill?

Not without even trying! So let's get invasive...

 <img src="https://user-images.githubusercontent.com/7414650/118323260-a226a080-b500-11eb-8e8f-3770aabdf15b.jpg" height="300" >  <img src="https://user-images.githubusercontent.com/7414650/118323305-b36fad00-b500-11eb-941a-776895bb2d11.jpg" height="300" > 

Five little testpoints! I have an urge to attach colorful wires... 

<img src="https://user-images.githubusercontent.com/7414650/118323326-bb2f5180-b500-11eb-9195-4a9cc7f2b5d9.jpg" height="300" >

... and do a little guesswork on what their purpose may be:

| Pin | Color of my cable | Shelly PIN| connect to|
|---|---------------------|-----------|------------|
|0  | violet              | GND       |  GND       |
|1  | blue                | GPIO0     |  GND       |
|2  | green               | VCC       |  3.3V      |
|3  | yellow              | TX        |  RX        |
|4  | orange              | RX        |  TX        |


Voila, it can be flashed:


```
Retrieving maximum program size .pioenvs/shelly_vintage1/firmware.elf
Checking size .pioenvs/shelly_vintage1/firmware.elf
RAM:   [====      ]  41.5% (used 33968 bytes from 81920 bytes)
Flash: [====      ]  42.0% (used 430208 bytes from 1023984 bytes)
======================================================== [SUCCESS] Took 3.24 seconds ========================================================
INFO Successfully compiled program.
Found multiple options, please choose one:
  [1] /dev/ttyUSB0 (USB-UART Controller)
  [2] Over The Air (shelly_vintage1.local)
(number): 1
INFO Running:  esptool.py --before default_reset --after hard_reset --baud 460800 --chip esp8266 --port /dev/ttyUSB0 write_flash 0x0 shelly_vintage1/.pioenvs/shelly_vintage1/firmware.bin
esptool.py v2.8
Serial port /dev/ttyUSB0
Connecting........_
Chip is ESP8266EX
Features: WiFi
Crystal is 26MHz
MAC: ...
Uploading stub...
Running stub...
Stub running...
Changing baud rate to 460800
Changed.
Configuring flash size...

A fatal error occurred: Timed out waiting for packet header
INFO Upload with baud rate 460800 failed. Trying again with baud rate 115200.
INFO Running:  esptool.py --before default_reset --after hard_reset --baud 115200 --chip esp8266 --port /dev/ttyUSB0 write_flash 0x0 shelly_vintage1/.pioenvs/shelly_vintage1/firmware.bin
esptool.py v2.8
Serial port /dev/ttyUSB0
Connecting........_____....._
Chip is ESP8266EX
Features: WiFi
Crystal is 26MHz
MAC: ...
Uploading stub...
Running stub...
Stub running...
Configuring flash size...
Auto-detected Flash size: 2MB
Flash params set to 0x0330
Compressed 434368 bytes to 300770...
Wrote 434368 bytes (300770 compressed) at 0x00000000 in 26.6 seconds (effective 130.8 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...

```

Unfortunately for everyone who is interested in the inner workings of this device, this little teardown ends here... I hope you had as much fun, as I had.

Best,
Richard


