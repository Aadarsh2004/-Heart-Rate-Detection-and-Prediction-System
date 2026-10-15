# ECG Heart-Rate Detector

Takes a noisy synthetic ECG sampled at 250 Hz (baseline drift, 50 Hz mains
interference, random noise), filters it, detects R peaks and computes heart
rate in bpm. Because the heart rate is known in advance, the result can be
checked against the true answer.

## Files
- `ecg.ipynb`: code, checks and plots
- `requirements.txt`: packages (numpy, scipy, matplotlib, pytest, ipykernel)

## Method
1. Generate synthetic ECG with a known heart rate (72 bpm)
2. Band-pass filter 0.5-30 Hz (Butterworth, order 4)
3. Detect R peaks with scipy.signal.find_peaks
4. Heart rate = 60 / mean RR interval

## Result
True 72 bpm, estimated 72.0 bpm.

## What went wrong
My first filter (2nd order, 40 Hz upper limit) did not remove the 50 Hz
mains noise well enough, so my 50 Hz check failed. A 4th-order filter with a
30 Hz upper limit fixed it.

## Limitations
Synthetic data is cleaner than real ECG. Next step: test on real data.