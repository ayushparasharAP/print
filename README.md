# print

**type 3 vs type 4**
PRINT DRIVERS
Print drivers is a layer that software into a translate Windows output in a language that a printer can understand.
Print drivers are provided by the printer manufacturers based on the model of the printer.
Print drivers are of two types:
Type 3 (Legacy)
Type 4 (Modern driver)
Type 4 drivers
1).Modern Print Class Drivers
2.) Provided through Windows Update 
3)simplified printer management A wide range of printers are supported due to common PDLs (PCL, PS, XPS)
4.) Take less space and are lighter
5.) Microsoft works with IHVs (Independent Hardware Vendors) to develop v4 drivers
6.) Less prone to crashes due to reduced driver size
7.) Updates can be done via Windows Update
Type 3 Drivers
1.) Legacy
2.) Provided by vendor / printer manufacturer
3.) Complex printer management For example: 32-bit & 64-bit drivers
Different drivers for different printer models
4.) Take more space (due to Microsoft’s configuration files)
5.) Developed by printer manufacturer
6.) More prone to crashes
7.) Updates of printer driver are manufacturer’s responsibility


**Client side rendering vs server side rendering**
Client-Side Rendering
It is a feature that allows print jobs to be fully rendered on the client when targeting a shared printer hosted on a Windows print server (client/server computing).After being rendered on the client, the print job is sent to the print server for queuing and printing by the print spooler, without further server-side rendering.
Server-Side Rendering
When printing through the print server, instead of the print job being rendered on the client, the job is directly sent to the print server, where the job gets rendered and sent to the print spooler for queuing and printing


**Print nightmare**
Print Nightmare is a known vulnerability in the Print Spooler service, which allowed attackers to execute code remotely and gain local privileges.
Fix / Patch
To fix this vulnerability, Microsoft released an update on 6th July 2021, introducing the registry key:
RestrictDriverInstallationToAdministrators (RDITA)
This value was set to 0 (Disabled) by default until Microsoft released another update on 10th August 2021, where this value was set to 1 (Enabled) by default.
Effect of This Setting
This registry key (RDITA) restricts standard users from installing printer drivers from a print server.

**Point & Print**
Point & Print is a feature that allows users to print to a remote printer or a network printer without having to manually download and install the printer driver on the machine.
How It Works
It checks for an existing printer driver on the local machine, and if it does not find a compatible driver, it downloads and installs the driver from the print server itself.



**PRINT FILTER PIPELINE**
⇒ It is an XPS-based print driver process. It processes the XPS spool file and includes the processing filters and the filter configuration file.
⇒ It is the logical collection of filters that are specified in the filter configuration file.
Filter Pipeline
ⅰ) Specifies filters to load
ⅱ) Processes job
ⅲ) Unloads filters
ⅳ) Exits or processes another job
Filter Pipeline Configuration Service
⇒ PrintFilterPipelineSvc.exe


**WSD (Web Services on Device)**
⇒ It is a protocol for communicating with a device (in this case, a printer) over the network.
⇒ WSD allows network-connected IP-based devices to advertise their functionality and offer these services to clients by using the web services protocol.
⇒ WSD provides a plug-and-play experience that is similar to installing a network device



**PRINTER REDIRECTION**
⇒ Printer Redirection is a feature that allows a local printer to be mapped on a remote machine, enabling printing across a network or the internet.
⇒ It enables users to print to their locally installed printer from a Terminal Services (Remote Desktop) session.
⇒ When a user connects to a remote system, their local printers are automatically redirected and appear in the remote session.
⇒ The print job is sent from the remote machine back to the user’s local system and printed on the local printer.


**Enhanced Point & Print**
Enhanced Point & Print is an updated printer sharing mechanism in Windows that allows client systems to connect to shared printers using V4 drivers, without downloading or installing manufacturer-provided drivers from the print server, thereby improving security and simplifying driver management.


**PRINTER DRIVER components**
PRINTER DRIVER INCLUDES
1. RENDERING COMPONENTS
2. CONFIGURATION COMPONENT
Rendering component
→ It converts the graphic commands from the application into a format that the printer understands
Configuration component
→ It contains a user interface (UI) that allows users to control printer settings & selectable options. It also includes a program interface that communicates the printer's configuration & features to the application


**Print Driver Isolation**
It allows admins to troubleshoot issues with printer drivers by isolating the print driver in a separate container.
PrintIsolationHost.exe is used for isolation.
There are 3 types of driver isolation:
None – Print driver is not isolated
Shared – Multiple print drivers are isolated in a shared container
Isolated – Each print driver is isolated in a separate container

**Remote Desktop Easy Print**
It was Previously known as TSEasyPrint, is used for redirecting printers on a remote computer.
For the redirected printer on the remote computer, this driver is used to send the print jobs to the printer that is connected.

**MOPRIA CERTIFIED PRINTERS**
MOPRIA CERTIFIED PRINTERS (Driverless Printers)
When a driver is not available, Windows can install Mopria Certified printers without needing to install any additional software or drivers.
MOPRIA (Mobile Printer Alliance)
It is an alliance of printer manufacturers that are working to define an open standard for driverless printing that can be used to make printing from mobile devices easier.
The Mopria Print Specification is an implementation of the Internet Printing Protocol (IPP) standard.


**HARDWARE ID**
It is an identifier assigned by the enumerator associated with the port that the printer is connected to.
A hardware ID is a vendor-defined identification string that Windows uses to match a device to an INF file.
A device can have more than one hardware ID associated with it.

**11b and handshake** 
Initial communication between print server and client was done on Port 445.
Now this communication happens over TCP 135 (RPC).
49152–65535 → Ephemeral ports
RPC
Client <--> Print Server
3-way handshake
Client sends request
Server acknowledges
Server assigns a random port from range
Client acknowledges back

0x11B
Both client & server Windows need to be on same patch. If not, when trying to add printer they are likely to get an error 0x11B.
If everything is fine (both are on the same patch) and still getting error 0x11B, it could be a network error or the port range could be blocked.




**connection flow for printing**
When we give a command to print on any application, if the data is only plain text, it goes to winspool.drv, which is called the client spooler interface.
If the data to be printed contains graphics, then the request goes to GDI (Graphics Device Interface). GDI converts the data into a form that is understood by winspool.drv.
2) After Conversion
After the conversion, the request goes to winspool.drv (which is an interface for the spooler). It calls the Spooler service (spoolsv.exe).
The Spooler service is a crucial component of the Windows OS that manages print jobs. Here, the printing process actually starts.
3) Spooler Service → spoolss.dll
The Spooler service calls spoolss.dll, which does the job of routing to a particular appropriate print provider.
The router determines which print provider to call based on the printer name or handle.
4) Print Providers
The router then calls the required print provider.
Print providers are implemented as Dynamic Link Libraries (DLLs).
These are of two types:
localspl.dll
win32spl.dll
NOTE: The default print processor in Windows is winprint.dll
localspl.dll → Handles print jobs for printers connected locally
win32spl.dll → Handles print jobs for printers on Windows network servers
Print providers direct print jobs to their correct destination, whether those destinations are local printers or network printers.
5) Print Processor
The print job is then directed to the print processor.
The print processor is where conversion from Enhanced Metafile (EMF) to RAW format takes place.
The print processor converts the spooled data of a print job into a format that a print monitor can send to the printer.
This conversion is necessary because applications generate print data in various formats, and printers require specific data formats to print.
The print processor also:
Reads the spool file
Performs necessary conversion operations on the data stream
Writes converted data back to the spooler
It also handles application requests to:
Pause
Resume
Cancel print jobs
6) Print Monitor
After conversion, the print processor sends data to the print monitor.
The print monitor is responsible for assigning jobs to ports on which the printer is connected.
7) Final Step
The processed print job is sent from the print spooler to the printer. It ensures the data is transmitted correctly and reliably to the printer.
The printer is the final destination and the physical device that produces hard copy output
The processed print job is sent from the print spooler to the printer. It ensures the data is transmitted correctly and reliably to the printer.
The printer is the final destination and the physical device that produces hard copy output.
**for network printing**
In network printing WIN32 Spl.dll the print provider from where the print job is directed to the spooler service (Spoolsv.exe) of the machine which has the printer connected to it locally.
From there the print job processes printing as it does in case of local. The print job is directed to the spooler service over port TCP 135 (RPC)



**SPOOLER COMPONENTS**
Application
The print application creates a print job by calling GDI functions.
GDI is used by applications that require graphics support or conversion.
Winspool.drv
This is a client interface into the spooler.
It is a driver file responsible for calling the spooler service.
Spoolsv.exe
It is implemented as a service where the OS is started.
Spoolss.dll
It acts as a router, determining which print provider to call based on the printer name or handle supplied with each function call.
Print Provider
The print provider is responsible for directing print jobs to local or remote print devices.
Types:
1. Local Spl.dll
Local print provider
Handles all print jobs directed to local printers
2. Win32 Spl.dll
Handles print jobs directed to remote servers
Print Processor
These convert spooled data from a print job into a format that is understood by the print monitor.
Note: Default print processor → Winprint
Print Monitor
It is responsible for directing the print data stream from the spooler to the specific port driver.
It is also responsible for management and configuration of printer ports on the server.


**Important points**
🔹 RDITA PATH
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Printers\Point and Print
🔹 RDITA (Important Policies)
Restrict Driver Installation to Administrators
RPC Authentication (Authn) Level Privacy Enabled
🔹 PRINTBRM.EXE
PrintBrm.exe → It is responsible for migrating printers from one system to another
🔹 EMF (Enhanced Metafile)
Enhanced Metafile is a description format defined by Microsoft for Windows.
It describes the appearance of text, graphical shapes, and sampled raster images on printed or displayed pages.
🔹 XPS (XML Paper Specification)
XPS → XML Paper Specification
🔹 SPLWOW64.EXE
SPLWOW64.EXE → Allows 32-bit applications running on 64-bit Windows to interact with 64-bit drivers
🔹 IMPORTANT REGISTRY KEYS
HKCU\Software\Microsoft\Windows NT\CurrentVersion\Devices
→ List of all printers installed
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print\Printers
→ Stores information on locally attached printers
🔹 DRIVER STORAGE LOCATIONS
Type 3 Drivers (Legacy)
C:\Windows\System32\spool\drivers\x64\3
Type 4 Drivers
C:\Windows\System32\spool\V4Dirs

****What are the various methods of Point & Print?**
**How can a printer be added/installed from print server?**
From Printers & Scanners (from Windows Settings)
UNC path
Drag & Drop
Right Click














