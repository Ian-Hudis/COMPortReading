Serial Bridge


-Get to the right folder location.
cd C:\Program Files (x86)\com0com

- Com to tcp server line.
C:\Program Files (x86)\com0com>com2tcp-rfc2217 \\.\CNCA0 localhost 7000

- Connecting comports.
hub4com --octs=off --baud=9600 --route=0:All \\.\COM3 \\.\CNCB0 \\.\CNCB1


General serial port solution.
// part 1
hub4com --octs=off --baud=9600 --bi-route=0:1 --route=0:2 --route=1:2 \\.\CNCB2 \\.\CNCB0 \\.\CNCB1

// part 2
com2tcp-rfc2217 \\.\COM6 localhost 7000


Wiring up Com4
 
•	By default, com0com has all the full rs232 connections. Com4hub does not do this by default because it is emo. 
// The Filter
--create-filter=pinmap:--dtr=dsr 
--create-filter=pinmap:--dtr=dcd 
--create-filter=pinmap:--ri=ri 
--add-filters=0:pinmap 
--add-filters=1:pinmap 
--route=0:1 --route=1:0 


Apply for the Arduino demo.

// part 1
hub4com --octs=off --baud=115200 --create-filter=pinmap:--dtr=dsr --create-filter=pinmap:--dtr=dcd --add-filters=0:pinmap --add-filters=1:pinmap --bi-route=0:1 --route=0:2 --route=1:2 \\.\COM3 \\.\CNCB0 \\.\CNCB1
// part 2
com2tcp-rfc2217 \\.\COM6 localhost 7000

Apply for a machine that uses Flow Control (might happen)

// part 1
hub4com --octs=off –XON=on --baud=115200 --create-filter=pinmap:--dtr=dsr --create-filter=pinmap:--dtr=dcd --add-filters=0:pinmap --add-filters=1:pinmap --bi-route=0:1 --route=0:2 --route=1:2 \\.\COM3 \\.\CNCB0 \\.\CNCB1
// part 2
com2tcp-rfc2217 \\.\COM6 localhost 7000


Procedure
-Step 1:  Inspection
Identify the physical com port the machine is using and how to switch the com port on the software machine interface and what baud rate and serial settings it is set to. Also obtain admin privileges otherwise the rest of the procedure will be like swimming in cement.
-Step 2: Install Com0com	
Install com0com_X64_Signed  on the computer.
-Step 3: Make Virtual Ports
Go to com0com/setupg.exe in Program Files (x86) and set up the virtual com ports. On the com port that is going to be used by the machine interface (COM4) check the “use Ports class.” For all connections check the emulate baud rate. Set COM4 to CNCB0 and COM6 to CNCB1. Check the Device manager to make sure it looks like below.
 
 

Step 4: Install Hub4com
	You just unzip it there is no real installation process. 
 
Step 5: Run script.
	Make changes to the .bat files that are necessary. You might need to change serial settings, motion control settings, TCP address, and TCP port. Then Run the script file to run the services in the background. To automate this process, attach the script to task scheduler or something. 

