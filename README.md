# Phase-Modulation-using-NumPy-and-Matplotlib

### Aim
To implement and analyze phase modulation (PM) using Python's NumPy and Matplotlib libraries.   
### Apparatus Required
1.	Software: Python with NumPy and Matplotlib libraries  
2.	Hardware: Personal Computer Theory  
Phase Modulation (PM) is a technique where the phase of the carrier wave is varied in proportion to the instantaneous amplitude of the input signal (message signal). Unlike frequency modulation, where the frequency is varied, in phase modulation, the phase angle of the carrier wave changes with the amplitude of the message signal.  

The general form of a PM signal can be represented as:


<img width="306" height="241" alt="image" src="https://github.com/user-attachments/assets/b8d2db63-afe0-4bd8-8826-efc89a111423" />

### Algorithm

1.	Initialize Parameters:  
o	Set values for carrier amplitude (AcA_cAc), carrier frequency (fcf_cfc), message frequency (fmf_mfm), sampling frequency, and phase deviation sensitivity (kpk_pkp).  
2.	Generate Time Axis:  
o	Create a time vector for the signal duration based on the sampling frequency.  
3.	Generate Message Signal:  
o	Define the message signal as a cosine wave.  
4.	Generate PM Signal:  
o	Apply the PM modulation formula to obtain the modulated signal.  
5.	Plot the Signals:   
o	Use Matplotlib to plot the message signal, carrier signal, and phase-modulated signal.  


### Program
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, filtfilt

Am = 7
Ac = 14
fm = 653
fc = 6530
fs = 65300

t = np.arange(0, 0.01, 1/fs)

kp = 0.5  
m = Am * np.cos(2 * np.pi * fm * t)
c = Ac * np.cos(2 * np.pi * fc * t)
pm = Ac * np.cos(2 * np.pi * fc * t + kp * m)

dpm = np.gradient(pm)

env = np.abs(dpm)
def butter_lowpass_filter(data, cutoff, fs, order=5):
    nyq = 0.5 * fs
    normal_cutoff = cutoff / nyq
    b, a = butter(order, normal_cutoff, btype='low', analog=False)
    return filtfilt(b, a, data)

cutoff = 2000  # low pass cutoff (must be > fm)
demod = butter_lowpass_filter(env, cutoff, fs)
demod = demod / np.max(demod) * Am


plt.figure(figsize=(10, 9))

plt.subplot(4, 1, 1)
plt.plot(t, m)
plt.title("Message Signal")
plt.ylabel("Amplitude")
plt.xlabel("Time (s)")

plt.subplot(4, 1, 2)
plt.plot(t, c)
plt.title("Carrier Signal")
plt.ylabel("Amplitude")
plt.xlabel("Time (s)")

plt.subplot(4, 1, 3)
plt.plot(t, pm)
plt.title("Phase Modulated Signal")
plt.ylabel("Amplitude")
plt.xlabel("Time (s)")

plt.subplot(4, 1, 4)
plt.plot(t, demod)
plt.title("Demodulated Signal (Recovered Message)")
plt.ylabel("Amplitude")
plt.xlabel("Time (s)")

plt.tight_layout()
plt.show()
```
### Tabulation
![515765994-f37d6ea4-4b92-4270-b739-5d421ab2e08f](https://github.com/user-attachments/assets/7597a605-33ad-425e-9d0c-33e6f2214d26)

### Output
<img width="989" height="890" alt="515766100-ac260dd1-ca27-478c-9cf6-a9f5e2964383" src="https://github.com/user-attachments/assets/46b73d3f-1ea6-4bea-8fbb-2ab39ff5e54c" />

### Result
The message signal, carrier signal, and phase-modulated (PM) signal will be displayed in separate plots. The modulated signal will show phase variations corresponding to the amplitude of the message signal.


