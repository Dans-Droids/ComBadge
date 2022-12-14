
![image](https://user-images.githubusercontent.com/72343266/204059726-b489b27e-8249-4f7a-ad3c-b7bba65312fd.png)

This is an ESP32-WROOM powered Communications Badge. Inspired by and based on Star Trek Lower Deck's ComBadge.
No copyright infringment intended, this is purely an exercise in fun and an homage to some great Sci-Fi Technology!


Hardware:
```
ESP32-WROOM-32e
OEP3W amp
8ohm Speaker (20mm x 14mm x 3mm)
200mah Lipo (15mm x 20mm x 5mm)
INMP441 I2S Mic (14mm OD)
3D Printed Case
Metal Adhesive Tape 38mm x 63mm to attach to Front.stl
or
Metal 3D print of Front.stl

```
## Hardware Setup
```
In Version 1, the components are just floating inside the case,
there is no PCB or proper support designed for the components due to the small size constraints.

Also the ESP32-WROOM-32e needs a separate devboard in order to program the firmware. 
(Search for ESP32-WROOM Programmer Devboard)

If using Metal Tape for Front.stl, there needs to be a piece of Metal Tape that bends round under the Front.stl
to the back and solder the TouchPin cable to this.

If using Metal Front.stl, you need to solder or screw the TouchPin cable to the rear-side.
The rear-side will need to be insulated before mounting components, Powder-Coat or Tape will be fine for this.

```

## Code & Libraries
```
The Voice Recognition is done by a pre-trained model using this page as a guide:
https://www.hackster.io/tinkerdoodle/deep-learning-speech-commands-recognition-on-esp32-b85c28?f=1

DAC is used to play audio over the OEP3W as all the I2S amps available were too big for the ComBadge, more info:
https://bigl.es/friday-fun-adafruit-chainsaw/

OTA Updating was modified from here:
https://github.com/rdehuyss/micropython-ota-updater

Capacitive Touch is built-in to the ESP32 so no external modules like the MPR121 were needed!

The multi-function Taps are a modification of the built-in PushButton library, here:
https://forum.micropython.org/viewtopic.php?t=8447



```



## Installation

```
OTA Update searches GitHub for the latest Release on BOOT.
If one is found it automatically Downloads, Installs
and Reboots the ComBadge - providing there is WiFi connection.

Else if building for first time, Flash firmware with thonny/etc, upload files and reboot. 
```

## Usage

```
Single-Tap (Tap and Release to register)
Double-Tap (tap twice within 400ms)
Hold-Tap (1 second hold)


Single tap on the Capacitive Touch Surface wakes from deep_sleep,
Plays the "Chirp.wav" and activates "Listening Mode".

In "Listening Mode" there are 5 Spoken Commands:
- Status
- Record
- Broadcast
- Call
- Update

STATUS speaks the Time, Internal Temperature Sensor, Battery Level & Connection Status.

RECORD begins recording from the microphone & writes to a file until
a Double-Tap is registered or 5 minutes elapse.

BROADCAST is the same as a Walkie-Talkie with a Hold-Tap acting as Push-To-Talk.
Double-Tap will end Broadcast Mode.

CALL will enable 1-to-1 communication based on number of taps to denote contact number 0-10,
given after "Call" Command is spoken.

UPDATE will force the ComBadge to REBOOT and check for an Update.
```

## ToDo
```
- Make simple starter file to run OTA updater, pulling latest Release to flash full working code. - DONE

- Test ESP-NOW firmware for better Broadcast functionality. - WIP

- Design PCB for Version 2 - DONE

- Bluetooth Classic HFP (Hands Free Protocol) for Mobile Phone passthru -WIP

- Expand 5 Phrases to more including peoples names, internet searches, math questions etc - WIP

- sync function to learn new "Contacts" within distance (maybe bluetooth pairing for safety) - WIP

- Find better battery/power solution - WIP
  Current: 220mah LiPo, USB-C Charging
  Proposed: SuperCapacitor(s) inside ComBadge, charged over wireless by undershirt magnet backing (MagPack) with built-in battery..USB-C charging on MagPack



```


## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.
