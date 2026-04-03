# Digital-Signal-Processing--Design-of-Chebyshev-Filter
## AIM:
To design of 2nd order Low Pass Chebyshev Filter using using Bilinear Transformation 
## SOFTWARE REQUIRED: 
MAT LAB R2012
## ALGORITHM: 
Step 1: Open MAT LAB. Write the program. 

Step 2: Read the values of Ap,As,Pass band frequency,Stop band frequency.

Step 3: Initialise some conditions to find out the order (N) value.

Step 4: Find out the transfer function of the filter and magnitude of that filter. 

Step 5: Plot the magnitude spectrum with x-label and y-label with suitable title. 

Step 6: Terminate the program. 

## PROGRAM:
```
clc;
clear all;
close all;

% Given values
Ap = 0.8;
As = 0.3;
wp = pi/2;
ws = 0.7*pi;
T  = 0.5;

% Pre-warping (Bilinear)
omega_p = (2/T)*tan(wp/2);
omega_s = (2/T)*tan(ws/2);

% Convert to dB
alpha_p = -20*log10(Ap);
alpha_s = -20*log10(As);

% Filter order and cutoff
[N, wc] = cheb1ord(omega_p, omega_s, alpha_p, alpha_s, 's');

% Normalized transfer function
[num, den] = cheby1(N, alpha_p, 1, 's');
disp('Normalized Transfer Function');
hs = tf(num, den)

% Unnormalized transfer function
[num1, den1] = cheby1(N, alpha_p, wc, 's');
disp('Unnormalized Transfer Function');
hs1 = tf(num1, den1)

% Bilinear transformation
[numz, denz] = bilinear(num1, den1, 1/T);
hz = tf(numz, denz, T);
disp('Digital Transfer Function');

% Frequency response
w = 0:pi/16:pi;
y = freqz(numz, denz, w);

% Plot
plot(w/pi, abs(y), 'b', 'LineWidth', 1.5);
xlabel('Normalized Frequency');
ylabel('Magnitude');
title('Chebyshev Low Pass Filter (Bilinear Method)');
grid on;
```


## OUTPUT:
<img width="702" height="522" alt="image" src="https://github.com/user-attachments/assets/d68525ef-7b92-4430-9dd1-b245f225b5b6" />


## RESULT:
<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/15017df4-8a66-492b-ad56-123e17837d06" />


