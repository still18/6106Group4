# Project Overview

## Motivation

Separating frequency bands and apply different FX chains on them is a tedious task, sometimes even impossible to do so in some DAWs. Yet it provides exciting possibilities, as shown by successful plugins like OTT and FabFilter Saturn 2. Multipass is a plugin that already provides such functionality. Unfortunately, it only supports loading plugins that also come from the same manufacturer: Kilohearts. If we can simply load our prebuilt effects?

We are aiming to create an application that can split signals into frequency bands and provides interactive user interface to modify plugin parameters in real time and hear the effect. Here are some problems that we must solve:

- Designed to load self-contained effects and chain them up. Calculate latency compensation correctly. Leave the interface open for loading third party plugins.
- If time permits, we will include the following two features for 3rd-party plugin support:
  - Scan VST plugins and allows users to select the VST they want to load.
  - Store and load serialized plugin states.
- Create an interactive frequency band split widget.

## Applications, use cases, and target users 

The target users for our application are individual vocalists. These vocalists often need to rely on external dependencies such as a DAW to get the correct modifications to their sound that they want. Our plan is to have a standalone application with built in effects, so that a user can experiment with different FX chains. 

## Functionality from user point of view and how it differentiates from similar products 

-	Split frequency bands
-	Scan and list plugins from third parties
-	Add plugins into plugin chain on each band
-	Pre & Post FX chain
-	Allows to adjust pan & volume & stereo separation (mid/side) of each band
-	Custom operation by users

## Plans for implementation

### Flow Chart

The flow chart already includes processor blocks.

![flow_chart](flowchart.png)

### Needed components and potential need for 3rd-party libs

- Librarys for IIR filters.
- Visualization and UI.

## Algorithmic references 

- Frequency split algorithm 
  - [Linkwitz Riley Filter](https://docs.juce.com/master/classdsp_1_1LinkwitzRileyFilter.html): cascaded 2nd-order Butterworth Low pass filters.
  - [`sosfiltfilt`](https://docs.scipy.org/doc/scipy/reference/generated/scipy.signal.sosfiltfilt.html)
- Compressor
  - RMS level detectors
  - Smoothing Filter
  - Expander and Compression
- Delay
  - IIR Filter comb filter design, input signal circulates into a delay line that is feedback to the signal chain 
  - [Echo effect reference](https://github.com/nxbyte/PythonAudioEffects/blob/master/AudioLib/AudioProcessing.py)
- Reverb
  -	FFT-based fast convolution? Block IR, then pre-calculate frequency response, finally overlap-add convoluted and IFFTed input signal block 
- Chorus & Flanger
  - Use an all-pass filter for the tap feedback
  - [flanger/chorus example](https://github.com/wybiral/python-musical)

## General Responsibilities and Work Assignments

For specific assignments, we will follow traditional SCRUM procedures by dividing up the work once we arrive at the start of a new Sprint. The Github issues for specific issues for given milestones will have individuals assigned to the specific tasks. For now we have designated basic directions for what we will work on:

- UI development and integration with filters, Chorus/Flanger effects (still18)
- DSP for the audio effects, I/O for the application, Compression effect (nol-alb)
- Basic concept experiment & validation including loading plugins or effectors, creating effector chains, and latency compensation. Plus Reverb effects, Delay effect (medioqrity, hchen605)

The SCRUM master will be rotated with sprints to allow for different perspectives at different stages.
