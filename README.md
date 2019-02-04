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

### Results

- The original noisy ECG signal is recorded using Bluetooth Configuration in MATLAB.

![](https://github.com/sharvaridesh/ECG-monitoring-using-capacitive-Electrodes/blob/master/results/ecg%20signal_1.JPG) |
|:--:| 
|*ECG signal obtained from the hardware circuit*|

There is discontinuity in first second of recorded data. In many cases, this discontinuous peak is much larger than all of the actual R-peaks, leading to incorrect R-peak detection. Thus, the first second of transient data is removed for each recording.

- Detrending of the recorded signal is done to fix the problem of baseline wander using a simple polynomial fit method.

![](https://github.com/sharvaridesh/ECG-monitoring-using-capacitive-Electrodes/blob/master/results/detrend.JPG) |
|:--:| 
|*Detrended ECG signal*|

- Digital Filtering 
  - Using an IIR Low pass filter, all the high frequency noises from the signal which are found mostly above 100Hz are removed. 
  - After LP filter, an IIR High pass filter to remove the low frequency noises usually found below a value of 0.7 Hz is used. 
  - A notch filter is used to eliminate the 60Hz Mains power Supply interference.

![](https://github.com/sharvaridesh/ECG-monitoring-using-capacitive-Electrodes/blob/master/results/detrend_lp.JPG) |
|:--:| 
|*ECG signal after detrending,low pass filtering*|

![](https://github.com/sharvaridesh/ECG-monitoring-using-capacitive-Electrodes/blob/master/results/hp.JPG) |
|:--:| 
|*ECG signal after detrending,low pass filtering, high pass filtering*|

![](https://github.com/sharvaridesh/ECG-monitoring-using-capacitive-Electrodes/blob/master/results/notch.JPG) |
|:--:| 
|*ECG signal after detrending,low pass filtering, high pass filtering, notch filtering*|

- After all the filtering is done, using the peak detection algorithm the R-peaks are obtained from the signal. It detects almost all the peaks correctly except for one since two of them appeared to be really close as seen from the figure below. 

![](https://github.com/sharvaridesh/ECG-monitoring-using-capacitive-Electrodes/blob/master/results/r-peak-detection.JPG) |
|:--:| 
|*R-peak detection*|

- Once the count of the R- peaks is acquired , the calculation of beats per minute (BPM) is carried out along with the graph for the heart rate variability (HRV). The results are shown in the figures below.

![](https://github.com/sharvaridesh/ECG-monitoring-using-capacitive-Electrodes/blob/master/results/bpm.JPG) |
|:--:| 
|*beats per minute calculated result*|

![](https://github.com/sharvaridesh/ECG-monitoring-using-capacitive-Electrodes/blob/master/results/hrv.JPG) |
|:--:| 
|*Heart Rate variability plot*|

- As an additional step, a Savitsky-Golay filter is used to smoothen out the signal further and is compared it to the original noisy signal.

![](https://github.com/sharvaridesh/ECG-monitoring-using-capacitive-Electrodes/blob/master/results/post-sg.JPG) |
|:--:| 
|*Savitzky-Golay filtered ECG signal*|
