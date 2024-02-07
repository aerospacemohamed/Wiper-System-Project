# Wiper-System-Project
System Description:
      Purpose: Simulate the behavior of a car wiper system based on driver input and rain sensor readings.
      Inputs:
          WprSys_vMode_Selector: Driver-selected mode (0: Off Mode, 1: Low Speed, 2: High Speed, 3: Automatic).
          WprSys_vWprSnsrErrRead_SC: Analog signal representing rain intensity.
          WprSys_bWprEna: Boolean indicating wiper on/off state.
          WprSys_sdl200ms: A scheduler that is used to trigger the system.
      Outputs:
          WprSys_WprMotDutCyc: Analog signal representing desired motor duty cycle.
          WprSys_bWprActv: Boolean indicating currently active mode (Off, Low Speed, High Speed, Automatic).
          WprSys_bModeErr: Boolean indicating the error status of the mode selector signal.
      Behavior:
          - The system updates every 200ms.
          - If WprSys_vMode_Selector changes and WprSys_bWprEna is true, the system waits for two subsequent WprSys_vMode_Selector readings.
          - If ModeSignal is "Automatic": The system uses 1D lookup table to map rain sensor value to WprSys_WprMotDutCyc based on automatic mode logic. 
          - Otherwise (Low Speed or High Speed):
               = For the Low-Speed Mode: The WprSys_WprMotDutCyc will be set to a calibrated value WprSys_WprMotDutCycLowSpd_SC that is set to (0.4).
               = For the High-Speed Mode: The WprSys_WprMotDutCyc will be set to a calibrated value WprSys_WprMotDutCycHighSpd_SC that is set to (0.7).
