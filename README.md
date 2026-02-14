# Ideal, Natural, & Flat-top -Sampling
# Aim
Write a simple Python program for the construction and reconstruction of ideal, natural, and flattop sampling.
# Tools required
# Program
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, filtfilt

fs=500
t=np.arange(0,1,1/fs)
m=np.sin(2*np.pi*5*t)

step=int(fs/50)
idx=np.arange(0,len(t),step)
w=int(fs/(2*50))

pulse=np.zeros(len(t)); pulse[idx]=1
ideal=np.zeros(len(t)); ideal[idx]=m[idx]
natural=np.zeros(len(t))
flat=np.zeros(len(t))

for i in idx:
    natural[i:i+w]=m[i:i+w]
    flat[i:i+w]=m[i]

b,a=butter(5,7/(0.5*fs),'low')
rec=filtfilt(b,a,flat)

plt.figure(figsize=(14,14))

plt.subplot(611); plt.plot(t,m); plt.title("Message"); plt.grid(True)
plt.subplot(612); plt.stem(t[idx],np.ones(len(idx)),basefmt=" "); plt.title("Sampling"); plt.grid(True)
plt.subplot(613); plt.stem(t[idx],ideal[idx],basefmt=" "); plt.title("Ideal"); plt.grid(True)
plt.subplot(614); plt.plot(t,natural); plt.title("Natural"); plt.grid(True)
plt.subplot(615); plt.plot(t,flat); plt.title("Flat Top"); plt.grid(True)
plt.subplot(616); plt.plot(t,rec); plt.title("Reconstructed"); plt.grid(True)

plt.tight_layout(); plt.show()

```
# Output Waveform
```
<img width="1660" height="551" alt="image" src="https://github.com/user-attachments/assets/867ac106-41b9-458e-8ac1-5b2090a8f539" />
<img width="1736" height="822" alt="image" src="https://github.com/user-attachments/assets/5659bb16-50b3-4fd0-a276-83829d4ba418" />
<img width="1660" height="303" alt="image" src="https://github.com/user-attachments/assets/4c48c312-c285-47d9-a932-cd2a8a4bdf78" />
```
# Results
```

```
# Hardware experiment output waveform.
