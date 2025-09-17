# Setting up the Prohelion WaveSculptor22

## Requirements: 
- Windows OS (Do not try linux you nerd)
- Prohelion Software ([Profinity](https://docs.prohelion.com/Profinity/index.html))
- [Peak USB-To-CAN drivers](https://www.peak-system.com/Drivers.523.0.html?L=1)
- A will to live

## Getting started: 
1. Open Profinity
2. Add peak adapter to profiles in Profinity
  - Click "Can Adapters"
  - Add the adapter (USB indicator should be green)
3. Add WaveSculptor22 to profiles
4. Add Virtual Can To Ethernet bridge (**you have to**)

## Configuration: 
1. Right-Click on WaveSculptor22 and click **Control and configure**
2. Click tools, phasesense (**needed for the motor to know how to spin**) (Only configure once)
3. (Optional) Manual motor control in `tools -> control`
