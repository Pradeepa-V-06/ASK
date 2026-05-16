# Amplitude-Shift-Keying And Frequency-Shift-Keying:
# Aim
Write a simple Python program for the modulation and demodulation of ASK and FSK.
# Tools required
Google Colab
# Program
# ASK
```
import numpy as np
import matplotlib.pyplot as plt

# Binary data
bits = [0,0,1,1,1,0,1,0,0,0]

# Parameters
samples_per_bit = 100
f = 5

# Time axis
t = np.arange(0, len(bits), 1/samples_per_bit)

# Message signal
message = np.repeat(bits, samples_per_bit)

# Carrier signal
carrier = np.sin(2 * np.pi * f * t)

# ASK Modulation
ask = message * carrier

# ASK Demodulation
decoded = []

for i in range(0, len(ask), samples_per_bit):

    segment = ask[i:i+samples_per_bit]

    if np.max(np.abs(segment)) > 0.5:
        decoded.append(1)
    else:
        decoded.append(0)

decoded_signal = np.repeat(decoded, samples_per_bit)

# Plotting
plt.figure(figsize=(10,8))

plt.subplot(4,1,1)
plt.plot(t, message, 'b')
plt.title("Message Signal")
plt.grid()

plt.subplot(4,1,2)
plt.plot(t, carrier, 'g')
plt.title("Carrier Signal")
plt.grid()

plt.subplot(4,1,3)
plt.plot(t, ask, 'r')
plt.title("ASK Modulated Signal")
plt.grid()

plt.subplot(4,1,4)
plt.step(t, decoded_signal, 'm')
plt.title("Decoded Bits")
plt.grid()

plt.tight_layout()
plt.show()
```
# FSK
```
import numpy as np
import matplotlib.pyplot as plt

# Binary data
bits = [1,1,1,1,1,0,1,1,0,0]

# Parameters
samples_per_bit = 100
f1 = 5     # Frequency for bit 0
f2 = 15    # Frequency for bit 1

# Total samples
N = len(bits) * samples_per_bit

# Time axis
t = np.arange(N) / samples_per_bit

# Message signal
message = np.repeat(bits, samples_per_bit)

# Carrier signals
carrier0 = np.sin(2 * np.pi * f1 * t)
carrier1 = np.sin(2 * np.pi * f2 * t)

# FSK Modulation
fsk = np.zeros(N)

for i, bit in enumerate(bits):

    start = i * samples_per_bit
    end = start + samples_per_bit

    if bit == 1:
        fsk[start:end] = carrier1[start:end]
    else:
        fsk[start:end] = carrier0[start:end]

# FSK Demodulation
decoded = []

for i in range(0, N, samples_per_bit):

    segment = fsk[i:i+samples_per_bit]

    zero_crossings = np.where(np.diff(np.sign(segment)))[0]

    if len(zero_crossings) > 10:
        decoded.append(1)
    else:
        decoded.append(0)

decoded_signal = np.repeat(decoded, samples_per_bit)

# Plotting
plt.figure(figsize=(10,10))

plt.subplot(5,1,1)
plt.plot(t, message, 'b')
plt.title("Message Signal")
plt.grid()

plt.subplot(5,1,2)
plt.plot(t, carrier0, 'g')
plt.title("Carrier Signal for bit = 0")
plt.grid()

plt.subplot(5,1,3)
plt.plot(t, carrier1, 'r')
plt.title("Carrier Signal for bit = 1")
plt.grid()

plt.subplot(5,1,4)
plt.plot(t, fsk, 'm')
plt.title("FSK Modulated Signal")
plt.grid()

plt.subplot(5,1,5)
plt.step(t, decoded_signal, 'k')
plt.title("Final Demodulated Signal")
plt.grid()

plt.tight_layout()
plt.show()
```
# Output Waveform

<img width="946" height="756" alt="image" src="https://github.com/user-attachments/assets/7443b35e-6a45-4686-a419-20ce3642b77a" />

<img width="857" height="830" alt="image" src="https://github.com/user-attachments/assets/5114986d-e5b2-449b-b8a6-0123564ab743" />

# Results
Thus, the ASK (Amplitude Shift Keying) AND FSK (Frequency Shift Keying) are performed using Google Colab
