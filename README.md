# Wavelength Division Multiplexing (WDM) Simulation

## Aim 
To simulate a WDM system using Python and analyze channel separation and insertion loss.

## Apparatus/Software Required
	Python (NumPy)
	Google Colab or Jupyter Notebook

## Theory
	WDM allows multiple optical signals at different wavelengths to be transmitted simultaneously over a single fiber.
	Channel spacing determines spectral efficiency and crosstalk.
	Insertion loss is the reduction in signal power due to multiplexing/demultiplexing.

## Formula:
"Insertion Loss (dB)"=P_in-P_out
"Channel Spacing"=Δλ

## 1
## Setup Environment
Info
Prepare Python environment for simulation.
	Import NumPy and Matplotlib
	Define channel wavelengths and powers

## 2
## Define WDM Parameters
Specify input wavelengths and powers.
Example: λ = [1550, 1552, 1554] nm, Pin = -2 dBm
	Choose 3 channels
	Assign equal input power

## 3
## Calculate Output Power
Simulate insertion loss for each channel.
Insertion Loss = Pin - Pout
	Assume ~1 dB loss per channel
	Compute Pout

## 4
## Plot WDM Spectrum
Visualize channel separation.
	Use Matplotlib to plot wavelength vs power
	Label each channel peak

## 5
## Analyze Results
Success
Interpret the simulation output.
	Channels separated with ~1–2 dB insertion loss
	Verify spacing Δλ = 2 nm

## Sample Output
 <img width="623" height="478" alt="image" src="https://github.com/user-attachments/assets/7569e8ec-3417-4669-b37b-06029f87655a" />

 <img width="677" height="466" alt="image" src="https://github.com/user-attachments/assets/e937804f-b55d-4de9-ab1e-155e6bd01d8e" />

 <img width="652" height="456" alt="image" src="https://github.com/user-attachments/assets/d22a7a99-0cd4-439e-b49b-b9dde93ab78b" />

## Python Code 
```
import numpy as np
import matplotlib.pyplot as plt

# Parameters
num_channels = 5
center_wavelength = 1550
channel_spacing = 0.8
bandwidth = 0.2

wavelength = np.linspace(1545, 1555, 2000)

# Generate channels
channels = []

for i in range(num_channels):
    lambda_i = center_wavelength + (i - num_channels//2) * channel_spacing

    spectrum = np.exp(
        -((wavelength - lambda_i)**2) /
        (2 * bandwidth**2)
    )

    channels.append(spectrum)

# Multiplexed signal
wdm_signal = np.sum(channels, axis=0)

# Individual channels
plt.figure()

for i, ch in enumerate(channels):
    plt.plot(wavelength, ch, linestyle='--', label=f'Ch {i+1}')

plt.xlabel("Wavelength (nm)")
plt.ylabel("Power")
plt.title("Individual WDM Channels")
plt.legend()
plt.grid()
plt.show()

# Combined WDM signal
plt.figure()
plt.plot(wavelength, wdm_signal)

plt.xlabel("Wavelength (nm)")
plt.ylabel("Power")
plt.title("Multiplexed WDM Signal")
plt.grid()
plt.show()

# Effect of channel spacing
spacings = [0.2, 0.8, 1.6]

plt.figure()

for spacing in spacings:
    channels = []

    for i in range(num_channels):
        lambda_i = center_wavelength + (i - num_channels//2) * spacing

        spectrum = np.exp(
            -((wavelength - lambda_i)**2) /
            (2 * bandwidth**2)
        )

        channels.append(spectrum)

    wdm_signal = np.sum(channels, axis=0)

    plt.plot(
        wavelength,
        wdm_signal,
        label=f'Spacing = {spacing} nm'
    )

plt.xlabel("Wavelength (nm)")
plt.ylabel("Power")
plt.title("Effect of Channel Spacing in WDM")
plt.legend()
plt.grid()
plt.show()
```

## Output
<img width="567" height="455" alt="image" src="https://github.com/user-attachments/assets/6a609645-111b-4980-833c-316de858dec0" />

<img width="567" height="455" alt="image" src="https://github.com/user-attachments/assets/77a231a3-6d9c-4c79-972e-e4dc54ce8372" />

<img width="567" height="455" alt="image" src="https://github.com/user-attachments/assets/a6854efa-597b-4fe8-8b9f-8f35881ad070" />

## Result 
The WDM system was successfully simulated using Python. Multiple optical signals with different wavelengths were multiplexed into a single optical channel and separated at the receiver. Channel separation and insertion loss were analyzed.
