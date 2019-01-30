# cap-electrodes
[![DOI](https://zenodo.org/badge/132076134.svg)](https://zenodo.org/badge/latestdoi/132076134)

Capacitive Electrodes team for ECE 522 (Spring 2018)

### Scripts
- `AT.ino`:   for configuring HC-05 Bluetooth module via AT commands
- `rtbt.ino`: for operating the Arduino Uno and HC-05
- `bt_ecg.m`: for collecting data from the Arduino Uno and analyzing it

### Setup
- configure baud rate of HC-05
  - check `AT.ino` for pinouts
  - remove Vcc of HC-05 and hold down button
  - reconnect Vcc. HC-05 should blink slowly
  - upload `AT.ino` and open serial monitor
  - set monitor to 9600 baud and type "AT+UART=115200,1,0"
- check the `rtbt.ino` for pin configurations of Arduino
- disconnect TX/RX
- upload `rtbt.ino`
- reconnect TX/RX
- run `bt_ecg.m`
