[README.md](https://github.com/user-attachments/files/33300715/README.md)
# WiFi Monitor

A touchscreen desk that shows your own Wi-Fi. The signal, a check to the router, a check out to the internet, download and upload speed, a clock, and a few names and addresses for that connection. The title on the glass says WIFI MONITOR.

It does not list the other devices in the house. The connections line is only a count of addresses that answered.

Two boards live in this folder. They are not the same screen. Do not flash one sketch onto the other board.

## 4.3 inch, Freenove FNK0115B

Sketch: `desklink43/desklink43.ino`

The screen is 480 by 272. Screen clock `9000000`, bounce `272 * 20`. The XPT2046 touch files sit beside that sketch. Prefs name is `link43`.

| Setting | Value |
| --- | --- |
| Board | ESP32S3 Dev Module |
| PSRAM | OPI PSRAM |
| Flash Size | 16MB |
| USB CDC On Boot | Enabled |

Use the Type-C port that shows up as CH340. Those rows are also in `desklink43/settings to change.txt`.

## 4.0 inch, Hosyond

Sketch: `desklink4/desklink4.ino`

ESP32-32E, ST7796S. Screen size 4.0 inch. Rotation 3, SD slot on top. The panel is 480 wide by 320 tall. The sketch draws in 800 by 480 and scales that onto the panel. Screen clock `20000000`. There is no extra RAM. Prefs name is `link4`.

The first time this screen is used, it asks you to touch four corners. That setup is stored under `xptcal` / `e32`. RESET on the Wi-Fi page forgets the network. It does not forget the corners.

This sketch does not use the XPT2046 library files from the 4.3 folder. Touch shares the screen's SPI bus.

| Setting | Value |
| --- | --- |
| Board | ESP32 Dev Module |
| Flash Size | 4MB |
| Partition Scheme | Huge APP (3MB No OTA) |
| Upload Speed | 921600 |
| Port | the COM port for this screen |

There is no second app slot on this board, so this size has no firmware update from GitHub.

## Libraries

GFX Library for Arduino, from the Library Manager. Wi-Fi, HTTP, and Preferences come with the ESP32 board package.

## What it shows

The buttons along the bottom are HOME, INFO, GRAPH, and WIFI. The INFO button opens a page titled LINK.

The clock comes from the internet after Wi-Fi connects. The place under the title is the location that came back with that connection. Until it arrives, the clock says `--:--` and the line says setting clock. There is no Pacific, Mountain, Central, or Eastern choice.

HOME shows the network name, signal bars, dBm, channel, download, upload, house milliseconds, internet milliseconds, the connection count, the internet company name when it comes back, the router name when the router gives one, this desk's address, the public address, the gateway, and the best, worst, and failed checks since midnight. On the 4.3 inch, DNS is on this page. On the 4.0 inch, DNS is on the LINK page.

Download and upload are how fast this desk moved a file over Wi-Fi for a few seconds. They are not the speed on the fiber bill. The first number can take a few seconds after joining. Then it checks again about every 3 minutes. `--` means that check has not finished.

GRAPH draws signal, download, and the internet check. Each title includes the latest number. A level line means that reading is holding steady.

WIFI is where you join the network. The 4.3 keyboard types small letters, numbers, and symbols. It has no capital-letter key. The 4.0 keyboard has abc for capitals, a symbol key, SCAN, and arrows through the network list. The password is visible on that page while you are typing it.

RESET clears the saved network on this desk and restarts it. It does not change the router or anything else in the house.

It needs 2.4 GHz Wi-Fi and USB power. There is no account.

## Listing

`etsy/` holds example screens, `ETSY-LISTING.txt`, and `WiFi-Monitor-User-Manual.pdf`. The names and numbers in the pictures are samples. The photos do not show a case or a stand.
