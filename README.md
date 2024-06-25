# EvilAppleWatch-ESP32S3
Spam BLE advertisements on iPhones with a ESP32S3 based smart watch! (Arduino IDE based project)

<img src="https://github.com/ShaunLinTW/EvilAppleWatch-ESP32S3/img/EvilAppleWatchDemo.JPG" width="300"><br>
<img src="https://github.com/ShaunLinTW/EvilAppleWatch-ESP32S3/img/EvilAppleWatchDemo-AVP.jpg" width="300"><br>

Based off of the work of [ronaldstoner](https://github.com/ronaldstoner) in the [AppleJuice repository](https://github.com/ECTO-1A/AppleJuice/blob/e6a61f6a199075f5bb5b1a00768e317571d25bb9/ESP32-Arduino/applejuice.ino) & [Raghu Saxena](https://github.com/ckcr4lyf) in the [EvilAppleJuice ESP32 repository](https://github.com/ckcr4lyf/EvilAppleJuice-ESP32/tree/master).

Also thanks to [simondankelmann](https://github.com/simondankelmann) for their discoveries in new advertising messages to pop-up new notifications in iOS devices [source](https://github.com/simondankelmann/Bluetooth-LE-Spam/blob/main/app/src/main/java/de/simon/dankelmann/bluetoothlespam/AdvertisementSetGenerators/ContinuityActionModalAdvertisementSetGenerator.kt)

With the randomization optimizations it can render an iPhone almost useless with a single ESP32S3 (a new notification as soon as you close the old one).

Confirmed on:
* iPhone 15 (running iOS 17.1.2)
* iPhone 14 Pro Max (running iOS 17.2 b3) (See #19)
* iPhone 14 Pro (running iOS 16.6.1)
* iPhone 13 Pro (running iOS 17.4 (21E5184k))
* iPhone 11 (running iOS 16.6.1)
* iPhone X (running iOS 14.8 (18H17)) - only "AppleTV Keyboard", "TV Color Balance", "AppleTV Setup", "AppleTV Homekit Setup", "AppleTV New User".
* iPad Pro 11 (running iPadOS 17.3 (21D50))

Not working on:
* iPhone 4S (running iOS 10.3 (14E277))
* iPhone 15 Pro/Pro Max(running iOS 18.0)

Other observations:
* Doesn't seem to spawn notifications if Keyboard is open / Camera is open

## Notable Differences

This implementation makes the following changes:

* Random source MAC address (including `BLE_ADDR_TYPE_RANDOM`)
* Randomly pick BLE Advertisement Type ([this may lead to more success](https://github.com/ECTO-1A/AppleJuice/pull/25))
* Randomly pick one of the possible devices
* Sets the ESP32S3 BLE Power to the maximum (9dBm) to increase range

And it makes these random choices every time it runs (default re-advertise every second).

Given the 29 devices and the 3 advertisement types, there are a total of 87 unique possible advertisements (ignoring the random source MAC) possible, of which one is broadcast every second.

## Usage

Clone the repo, and easiest would be to use Arduino IDE to upload it to your ESP32S3.

This project has been tested on an [ESP32-S3 from Waveshare](https://www.waveshare.com/esp32-s3-touch-lcd-1.28-b.htm).


