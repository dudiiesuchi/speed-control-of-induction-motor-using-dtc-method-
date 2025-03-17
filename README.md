# Direct Torque Control (DTC) of an Induction Motor in MATLAB

## Overview
This repository contains a MATLAB/Simulink-based implementation of Direct Torque Control (DTC) for an induction motor drive. DTC is a widely used technique for precise torque and flux control in AC motor drives.

## Electrical Model
The electrical energy is supplied by a three-phase AC/DC diode rectifier connected to a **460 V, 60 Hz** grid equivalent. The DC bus is connected to a **three-phase, two-level converter**, which generates the variable voltage and frequency required for variable-speed operation of the **150 HP induction motor**. Additionally, a **braking chopper** is connected to the DC bus to dissipate kinetic energy during deceleration.

## Control Techniques
An inverter-fed induction motor drive can be controlled through various techniques. Common methods include:
- **Scalar Control (V/Hz control)**
- **Vector Control (Field-Oriented Control or Direct Torque Control)**

This project specifically implements **hysteresis-based Direct Torque Control (DTC)**.

## Direct Torque Control (DTC) Strategy
DTC allows instantaneous control of motor **magnetic flux** and **electromagnetic torque** in a decoupled way. The main components of the DTC subsystem are:

### 1. Flux and Torque Calculation
- Stator flux linkage is estimated by integrating the stator voltages.
- Electromagnetic torque is calculated based on estimated flux and motor currents.

### 2. Speed Regulator
- Compares actual motor speed with the reference speed.
- Generates the torque reference to maintain the desired speed.

### 3. Hysteresis Control
- Compares calculated flux magnitude and torque with reference values.
- When flux or torque error crosses a hysteresis band, a control signal is activated to correct the error.

### 4. Optimal Switching
- Inverter switching pulses are generated based on control signals and stator flux linkage position.
- The appropriate voltage vector is selected dynamically depending on the flux linkage sector.

## Simulation Details
### Initial Conditions
- Flux reference is set to **0.9 V.s**.

### Timeline
- **0.1 s**: Speed reference set to **1500 RPM**, motor starts accelerating.
- **1.35 s**: Motor reaches **1500 RPM**.
- **1.5 s**: Load torque of **500 N.m** applied, DTC maintains speed.
- **2.0 s**: Load torque reduced to **50 N.m**.
- **2.5 s**: Speed reference reduced to **500 RPM**, braking chopper dissipates kinetic energy.
- **3.5 s**: Flux reference increased to **1.0 V.s**.

### Running the Simulation
To run the simulation in **MATLAB/Simulink**:
1. Open the MATLAB project and navigate to the Simulink model.
2. Run the simulation and observe the waveforms on Scope2.
3. Analyze the motor response and braking chopper behavior.

## Real-Time Simulation (Optional)
If using **Simulink Real-Time** and a **Speedgoat target computer**:
1. Open **Configuration Parameters** (Ctrl+E).
2. Navigate to **Code Generation** and set **System target file** to an STF for Simulink Real-Time.
3. Connect to the target and click **Run on Target** in the **Real-Time** tab.
4. Adjust the number of signals transferred to match the available bandwidth.

## References
1. M. Cirrincione, M. Pucci, G. Vitale. *Power Converters and AC Electrical Drives with Linear Neural Networks*. CRC Press, 2012.
2. ABB. *Technical Guide No. 1: Direct Torque Control - The World's Most Advanced AC Drive Technology*, 2011.
3. T. Wildi, G. Sybille. *Electrotechnique (4th edition)*. Les Presses de la Université Laval, 2005.
