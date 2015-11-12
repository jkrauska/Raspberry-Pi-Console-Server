# Raspberry-Pi-Console-Server
Notes and setup detail about setting up a Raspberry Pi to act as a Serial Console Server (Serial Concentrator)

## The Problem
Serial console servers have been around forever and always been curiously expensive.

The old ones out there are running ancient versions of ssh and ancient kernels and SHOULD NOT be on the public internet.

## Exploring using a Pi as a console server.

The parts are ordered.<br>
Pi 2, case, power adapter to micro-usb, 32GB micro sd, powered USB 2.0 hub, 4 USB to serial adapters, 1U shelf.
Total costs are under $200.  

Other parts to consider for possible future improvements:
 - Startech 4-port serial to USB 2.0(or 8-port or 16-port!)

Things to 'worry' about:
 - Cleanish wiring/access in a rack
 - Naming standard for USB/Serial ports.
 - Persistence of USB device names. (udev device names based on serial)
 - Easy ssh based console access (minicom? screen? tmux?)
 - Easy speed changing
 - https Web console to serial with auth of some sort
 - multiplex'd serial access (more than one user can watch/interact at the same time)
 - ssh port to serial port direct mapping (eg, port 2201 maps to serial 1)
 - logging/buffering stuff coming in serial port so it's there for the next login (show me the oops!)
 - packaging something nice in a ppa for raspberrian?
 - rolling a dedicated distro (please no)

VERY PROMISING -- 

console-server package does 80% of the work...
https://pypi.python.org/pypi/ConsoleServer
https://github.com/LawrenceK/console-server

this page documents a websockets approach to create a web serial console.
http://fabacademy.org/archives/2015/doc/WebSocketConsole.html



## Grumpy Network/Sysadmin in his 40s rambling on a bit...

It used to be that you took an old cisco 2500/2600 router with an aysnc interface and used an octopus 
cable and that was how you talked to serial consoles. (when you weren't just using an old school vt520 
amber serial terminal console to be cool like Libor.)

Then came Cyclades TS-3000s in the earlu 2000s, which was blue and sexy and cost a bit, but had 48 ports 
of serial and could do 115200 per port.  You could serial console up a whole rack of servers with clean 
cabling and 1U. These were pretty awesome since they were running linux, but Cyclades got bought up by 
Alterpath who was bought by Avocent and then eventually went to Emerson?

You can still get TS-3000s for around $100 on ebay, but just be warned that it's a 50Mhz powerpc 8xx 
chip with 128MB of RAM you're buying and you'll start to want someting better. 
(nevermind that the firmware updates seems to have stopped in 2008 -- http://www.emersonnetworkpower.com/en-US/Support/Software-Downloads/infrastructure-management/Legacy-Downloads/Pages/Cyclades-TS-Terminal-Servers.aspx)

In the late 2000s I became a big fan of Opengear.  They had much faster processors, still ran linux and 
had much nicer web interfaces. They would listen to bug reports and deploy fixes quickly.  They were also 
1/3 the cost of an Avocent ACS48. They still are a great option since they still cost less than any of your 
servers, but they still cost a bit too much imo.

Opengear has made a seemingly successful business out of writing awesome integrations with other common 
datacenter gear like PDUs, environmental monitors, etc. and they made it all easy to hook in to your existing
alerting infrastrucutre.  

But today I can get a quad core 900Mhz ARM pi with USB for $40.  And I've used those things for all sorts of
things but not yet a serial console server. Thus this project/notes/page.
