This is the README file for the jeap2 GitHub repository, which is the used for JEAP 2.0, an auto provisioning program for SRX series firewalls

ANY AND ALL FILES CONTAINED WITHIN THIS REPOSITORY ARE FOR INTERNAL USE OF CURRENT EMPLOYEES OF JUNIPER NETWORKS AS OF SEPTEMBER 3RD, 2015

THIS REPOSITORY AND ANY AND ALL FILES CONTAINED WITHIN ARE THE SOLE INTELLECTUAL PROPERTY OF THE OWNER, ADMIN, AND CONTRIBUTORS.

ACCESS TO OR USE OF ANY FILES, SCRIPTS, FUNCTIONS, OR OTHER MATERIAL CONTAINED WITHIN THIS REPOSITY IS STRICTLY AND EXPRESSLY
LIMITED TO AUTHORIZED OWNERS, ADMINS, CONTRIBUTORS, OR CURRENT EMPLOYEES OF JUNIPER NETWORKS UNDER A STANDARD EMPLOYEE NON-DISCLOSURE
AGREEMENT.

UNAUTHORIZED USE OR DISTRIBUTION OF ANY AND ALL FILES CONTAINED WITHIN IS STRICTLY AND EXPRESSLY FORBIDDEN.

USE OF THIS REPOSITORY AND ANY AND ALL FILES CONTAINED WITHIN IS SUBJECT TO THE FOLLOWING DISCLAIMER:

----------------------------------------------------------------------------
Copyright (c) 2015-2016  Juniper Networks. All Rights Reserved.

 YOU MUST ACCEPT THE TERMS OF THIS DISCLAIMER TO USE THIS SOFTWARE
 
 JUNIPER IS WILLING TO MAKE THE INCLUDED SCRIPTING SOFTWARE AVAILABLE TO YOU
 ONLY UPON THE CONDITION THAT YOU ACCEPT ALL OF THE TERMS CONTAINED IN THIS
 DISCLAIMER. PLEASE READ THE TERMS AND CONDITIONS OF THIS DISCLAIMER
 CAREFULLY.

 THE SOFTWARE CONTAINED IN THIS FILE IS PROVIDED "AS IS." JUNIPER MAKES NO
 WARRANTIES OF ANY KIND WHATSOEVER WITH RESPECT TO SOFTWARE. ALL EXPRESS OR
 IMPLIED CONDITIONS, REPRESENTATIONS AND WARRANTIES, INCLUDING ANY WARRANTY
 OF NON-INFRINGEMENT OR WARRANTY OF MERCHANTABILITY OR FITNESS FOR A
 PARTICULAR PURPOSE, ARE HEREBY DISCLAIMED AND EXCLUDED TO THE EXTENT
 ALLOWED BY APPLICABLE LAW.

 IN NO EVENT WILL JUNIPER BE LIABLE FOR ANY LOST REVENUE, PROFIT OR DATA, OR
 FOR DIRECT, SPECIAL, INDIRECT, CONSEQUENTIAL, INCIDENTAL OR PUNITIVE DAMAGES
 HOWEVER CAUSED AND REGARDLESS OF THE THEORY OF LIABILITY ARISING OUT OF THE 
 USE OF OR INABILITY TO USE THE SOFTWARE, EVEN IF JUNIPER HAS BEEN ADVISED OF 
 THE POSSIBILITY OF SUCH DAMAGES.

 ----------------------------------------------------------------------------

Owner/Admin:	Logan Donielson

Contributors:	Logan Donielson
				Maltimore Butler
				Michelle Zhang

Necesary software:	A UNIX server, physical or virtual, with DHCP and TFTP
					services configured, that also supports standard Bash commands.
					Python 2.7.10 or equivilant version


Necesary modules/libraries:	Pip (for installing necesary software and libraries)
							Requests (Python library)
							lxml (Python library)
							PyEz (Python library)
							BeautifulSoup4 (Python library)


Necesary files:	jeap.py
				scraper_bike.py
				lease_listen.py
				known_hosts.txt
				listen_execute.sh


Necesary initial config:

In your CentOS server, navigate to the
/etc/rc.d directory and edit the rc.local file.

Add the following command to the last line of rc.local:

while true; do ./listen_execute.sh; sleep 20; done

rc.local will execute all shell commands contained within itself
as soon as it starts up, but after it has initialized and executed
all other critical services and commands.

This command will loop infinitely, until the process is manually killed,
or the machine is shut down, and it will execute listen_execute.sh
every time it loops, which intern will check dhcp.leases for new
dhcp leases and retrieve the client IP addresses.

The "sleep 20;" portion of the command is used to specify how long
the system should wait in between each iteration of the loop,
which executes listen_execute.sh

"20" is the time interval, in seconds that the system will wait.
For instance, "sleep 10" will wait 10 seconds in between each
iteration of the loop, while "sleep 60" will wait 20 seconds.
You can modify this variable as you wish, although it is strongly
reccomended that you specify the wait time to be a minimum of 10 seconds
so that the other scripts that listen_execute.sh calls will have time to
execute themselves.


To all contributors: Please feel free to add any relevant information regarding this project
to the README. Just please use a format that is easily readable, and clearly label it.

