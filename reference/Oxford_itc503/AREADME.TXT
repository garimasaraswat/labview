Oxford Instruments

Instrument Drivers for LabVIEW version 8.5


Installation
------------

NB:
1) If using a USB serial converter, we recommend using one of industrial standard such as a "Brainbox" or one supplied by NI.
Please be aware that some USB-Serial converters may lose data (eg we have observed data losses when using Prolific).
Also, the Prolific USB-serial driver, in combination with NI-VISA versions newer than NI-VISA 4.2, may cause system crash.
2) Re LabVIEW Environment Options -
Please use the default setting for the "Automatically close VISA sessions" option, i.e. OFF (unchecked).


To install the software, unzip the zip file to a folder on your PC.

If you want to mass compile the VIs to the version of LabVIEw that you are using:
1. Start LabVIEW
2. Select Tools->Advanced->Mass Compile...
3. At the "Choose a directory to compile" dialog, navigate to the folder into which you unzipped the software and click on the "Current Folder" button (bottom right of the dialog)
4. At the "Mass Compile" dialog, click on the "mass compile" button.
5. Warning - there will be errors compiling several of the VIs (eg "Bad VI"). These errors do not matter. They occur because the individial instrument driver package is part of a larger package, and some of the VIs in your package refer to VIs in the larger package.


VIs for communicating with OI instruments may be found in .LLB files, as follows:
Instrument       Driver VIs	Driver Application
ITC502/503/601   ITCSUBS.LLB    ITCAPPS.LLB (eg ITCSetupDialog.vi, ITC503FrontPanel.vi)
IPS              PSSUBS.LLB     PSAPPS.LLB (eg PSSetupDialog.vi, IPSFrontPanel.vi)
LC               LCSUBS.LLB     LCAPPS.LLB (LambdaControllerSetupDialog.vi, LambdaControllerFrontPanel.vi)
SMC4             SMC4SUBS.LLB   SMC4APPS.LLB (SMC4SetupDialog.vi, SMC4FrontPanel.vi)
ILM              ILMSUBS.LLB    ILMAPPS.LLB (ILMSetupDialog.vi, ILMFrontPanel.vi)
ISS              ISSSUBS.LLB    ISSAPPS.LLB (ISSSetupDialog.vi, ISSFrontPanel.vi)


IO Info Cluster
---------------

When calling the driver VIs you need to supply a cluster of IO information.

All instrument VIs need address information:
1. Serial link direct to computer
	Communication:  RS232
	Com Port:       No of com port used
	ISOBUS address: -1
	GPIB address:   N/A
2. ISOBUS cable direct to computer
	Communication:  ISOBUS
	Com Port:       No of com port used
	ISOBUS address: set to unique non-zero value (see default ISOBUS addresses below)
	GPIB address:   N/A
3. ISOBUS connected via a Gateway instrument
	Communication:  Gateway
	Com Port:       N/A
	ISOBUS address: set to unique non-zero value (see default ISOBUS addresses below)
	GPIB address:   GPIB address of Gateway instrument
4. GPIB only
	Communication:  GPIB
	Com Port:       N/A
	ISOBUS address: 0
	GPIB address:   GPIB address
5. Instrument is acting as the Gateway instrument
	Communication:  Gateway
	Com Port:       N/A
	ISOBUS address: 0
	GPIB address:   GPIB address

NB We recommend use of National Instruments GPIB interfaces and cannot support use of other interfaces. 


Some instruments need more information:

1. ITC502/503/601
	Version:        ITC502/ITC503/ITC601
	Ch1 Name:       a name
	Ch2 Name:       a name
	Ch3 Name:       a name
	Ch1 dec places: decimal places for channel 1 (only for ITC4 or ITC502)
	Ch2 dec places: decimal places for channel 2 (only for ITC4 or ITC502)
	Ch3 dec places: decimal places for channel 3 (only for ITC4 or ITC502)

2. IPS/PS
	Version:        PS/IPS

3. SMC4
	No. of motors:  eg 1
An array of clusters, one array element for each motor. However, element 0 is unused - 
element 1 is for motor 1, element 2 is for motor 2 etc. Each cluster contains
	Name:           a name
	Steps/unit:     the number of motor steps taken for 1 Unit of travel
	Units:          Name of the units
	Lower limit:    The position in Units when the lower limit switch is active
	Upper limit:    The position in Units when the upper limit switch is active
	Speed:          The speed is a decimal number between 0 and 255, used to divide
                        the 1kHz clock rate to obtain the step rate.
			S0,1 = clock rate, S2 = clock rate/2


Default ISOBUS Addresses
------------------------
ITC502/503        - 1
PS***/IPS***      - 2
Lambda Controller - 3
SMC4              - 4
IGH               - 5
ILM200            - 6
ISS**             - 7


To find the address info for the instruments connected to your system:

1. Run INSTRUM.LLB/Search for Instruments.vi
2. Select GPIB or ISOBUS
3. If using ISOBUS, enter the number of the com port.
4. Click on the "Search for Instruments" button.
If any instruments are found they will be listed on the right of the dialog.
If any instruments share the same address there will be a device conflict.
Find the address of an individual instrument by powering off all instruments but the one whose address you want to check.


GMH 28 Apr 2010