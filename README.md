# print
na
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
