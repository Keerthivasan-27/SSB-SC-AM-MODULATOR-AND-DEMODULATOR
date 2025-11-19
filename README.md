# SSB-SC-AM-MODULATOR-AND-DEMODULATOR
## AIM

To write a program to perform SSBSC modulation and demodulation using SCI LAB and study its spectral characteristics
## EQUIPMENTS REQUIRED

•	Computer with i3 Processor

•	SCI LAB

Note: Keep all the switch faults in off position

## ALGORITHM
  1.	Define Parameters:
     
    •	Fs: Sampling frequency.
    •	T: Duration of the signal.
    •	Fc: Carrier frequency.
    •	Fm: Frequency of the message signal.
    •	Amplitude: Maximum amplitude of the message signal.
    
  2.	Generate Signals:
     
    •	Message Signal: The baseband signal that will be modulated.
    •	Carrier Signal: A high-frequency signal used for modulation.
    •	Analytic Signal: Constructed using the Hilbert transform to get the in-phase and quadrature components.

  3.	SSBSC Modulation:
     
    •	Modulated Signal: Create the SSBSC signal using the in-phase and quadrature components, modulated by the carrier.

  4.	SSBSC Demodulation:
     
    •	Mixing: Multiply the SSBSC signal with the carrier to retrieve the message signal.
    •	Low-pass Filtering: Apply a low-pass filter to remove high-frequency components and recover the original message signal.

  5.	Visualization:
     
    Plot the message signal, carrier signal, SSBSC modulated signal, and the recovered signal after demodulation.

## PROCEDURE

  •	Refer Algorithms and write code for the experiment.
  
  •	Open SCILAB in System
  
  •	Type your code in New Editor
  
  •	Save the file
   
  •	Execute the code
  
  •	If any Error, correct it in code and execute again
  
  •	Verify the generated waveform using Tabulation and Model Waveform
## MODEL GRAPH
<img width="747" height="338" alt="image" src="https://github.com/user-attachments/assets/dd117c5d-ee32-47c7-946c-df6180b0d33f" />

## PROGRAM
clc;
clear;
close;

// --- Parameters ---
Am = 14.7;
Ac = 29.4;
fm = 1453;
fc = 14530;
fs = 145300;
t = 0:1/fs:3/fm;                 // 3 cycles of message

// --- Message and SSB-SC signal ---
m = Am * cos(2 * %pi * fm * t);         // message (row vector)
m_h = imag(hilbert(m));                 // Hilbert transform
s_usb = m .* cos(2 * %pi * fc * t) - m_h .* sin(2 * %pi * fc * t); // USB

// --- Coherent detection ---
local_carrier = cos(2 * %pi * fc * t);
y = s_usb .* local_carrier;

// --- Low-pass filter (FFT method) ---
Y = fft(y);
N = length(Y);
f = (0:N-1)*(fs/N);
cutoff = 2*fm;
H = (f < cutoff);
Y_filtered = Y .* H;
y_demod = real(ifft(Y_filtered));

// --- Plotting ---
subplot(3,1,1);
plot(t, s_usb);
title("Received SSB-SC Signal");
xlabel("Time (s)"); ylabel("Amplitude");

subplot(3,1,2);
plot(t, y);
title("After Coherent Mixing");
xlabel("Time (s)"); ylabel("Amplitude");

samples_to_show = min(int(fs*0.001), length(y_demod));
subplot(3,1,3);
plot(t(1:samples_to_show), y_demod(1:samples_to_show));
title("Demodulated Message Signal (After LPF)");
xlabel("Time (s)"); ylabel("Amplitude");

// ✅ SSB-SC AM MODULATOR (Upper Sideband)
clc;
clear;
close;

// --- Parameters ---
Am = 14.7;
Ac = 29.4;
fm = 1453;
fc = 14530;
fs = 145300;
t = 0:1/fs:3/fm;          // duration for 3 message cycles

// --- Message and Carrier ---
m = Am * cos(2 * %pi * fm * t);      // Message signal
m_h = imag(hilbert(m));              // Hilbert transform (phase-shifted message)

// --- SSB-SC Modulation (Upper Sideband) ---
s_usb = m .* cos(2 * %pi * fc * t) - m_h .* sin(2 * %pi * fc * t);

// --- Plot Results ---
subplot(3,1,1);
plot(t, m);
title("Message Signal m(t)");
xlabel("Time (s)");
ylabel("Amplitude");

subplot(3,1,2);
plot(t, s_usb);
title("SSB-SC Modulated Signal (Upper Sideband)");
xlabel("Time (s)");
ylabel("Amplitude");

// ✅ Fix: Zoom-in region properly (first few ms)
samples_to_show = 1:int(fs*0.001);   // show first 1 ms
subplot(3,1,3);
plot(t(samples_to_show), s_usb(samples_to_show));
title("Zoomed-in View of SSB-SC Signal");
xlabel("Time (s)");
ylabel("Amplitude");

## TABULATION
![WhatsApp Image 2025-11-19 at 19 45 26_d86de475](https://github.com/user-attachments/assets/cc9c5021-d2c4-47be-a2d5-a92d891085bd)


## OUTPUT
![WhatsApp Image 2025-11-19 at 19 45 43_b13f887b](https://github.com/user-attachments/assets/cf3367cc-acad-4429-89da-a07e79b58085)

## RESULT
Thus the SSB-SC-AM modulation and demodulation is experimentally done and the output is verified


