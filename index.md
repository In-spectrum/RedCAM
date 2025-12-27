<h1 align="center">
	<a href="https://github.com/In-spectrum/RedCAM" target="_blank">
		<img src="manual/images/baner.png" width="750" height="250" alt='RedCAM | Personal media service.' >
	</a>
	<br>
	<a href="https://github.com/In-spectrum/RedCAM" target="_blank">
		Personal media service
	</a>
</h1>

<br>

**Purpose**
* to create personal media service for viewing, recording RTSP streams from video cameras;
* share the video stream with other users;
 
**Application was tested**
* <a href="https://github.com/In-spectrum/RedCAM/releases" target="_blank">Windows 10, Ubuntu 20.04.6, Android 11;</a>

**Planned**
* macOS;

## Table of contents

* [**RedCAM-server**](#RedCAM-server)
  * [Functions](#functions)
* [**RedCAM-client**](#RedCAM-client)
  * [Functions](#functions-1)
* [**License**](#license)

## **RedCAM-server**
### Functions  
  &emsp;&nbsp;- user registration;
  <br>&emsp;&nbsp;- recording video files;
  <br>&emsp;&nbsp;- user access to cameras and files (depending on the status);

## RedCAM-client
The administrator creates users and has access to all cameras.

### Functions
- adding/deleting RTSP streams of its cameras;
- simultaneous viewing of several video cameras;
- setting the total time for recording files;
- setting the status of the video camera as publicly available for all users on the server;
- generating code for viewing the video camera by clients who are not connected to the server but have the application  -installed.

### Features
- the server must be online (statistics are kept on the number of working RedCAM-servers);
- server usage, including in local networks, without collecting statistics is under development;
   
### Properties
**-pas** - set server password (default 1111); _**./RedCAMServer.sh -pas 2227**_<br>
**-p** - set listen port; _**./RedCAMServer.sh -p 1675**_<br>
**-la** - time to disconnect clients with low activity; _**./RedCAMServer.sh -la 60**_<br>
_<h style="font-size:8; ">&emsp;&emsp;&emsp;*if the client is connected and not in use, it will be disconnected from the server after 60sec.<br>
&emsp;&emsp;&emsp;&ensp;After 30sec the client will reconnect to the server to identification on the network.</h>_

### Install
 - download <a href="https://github.com/In-spectrum/RedCAM/releases" target="_blank">application archive</a> and unzip;
 - start the server with parameters:
<br>**_RedCAMServer.ехе -pas 2227 -p 1675 -la 60_** - for Windows;
<br>**_./RedCAMServer.sh -pas 2227 -p 1675 -la 60_** - for Ubuntu
<br>**_chmod +x RedCAMServer_** and run **_./RedCAMServer -pas 2227 -p 1675 -la 60_** - for Raspberry Pi

### Example script to check RedCAM-server

~~~
#!/bin/bash

sleep 10

a_pFNS_tcp=1137 #for RedCAMServer
a_pRTSP=8554 #for RTSP
a_pRTMP=1927 #for RTMP
a_pSSH=6744 #for SSH

# opening of ports
sudo systemctl start firewalld
sudo firewall-cmd --zone=public --add-port=${a_pSSH}/tcp --permanent #for SSH
sudo firewall-cmd --zone=public --add-port=${a_pRTSP}/tcp --permanent #for RTSP
sudo firewall-cmd --zone=public --add-port=${a_pRTMP}/tcp --permanent #for RTMP
sudo firewall-cmd --zone=public --add-port=${a_pFNS_tcp}/tcp --permanent #for RedCAMServer
sudo firewall-cmd --reload

while true
do
    # RedCAMServer check
    if pgrep "RedCAMServer" > /dev/null; then
        echo "RedCAMServer STARTED!"
    else
        echo "RedCAMServer NOT STARTED"

        cd /home/user/RedCAMServer
        ./RedCAMServer.sh -p ${a_pFNS_tcp} &
    fi

    # Mediamtx check
    if pgrep "mediamtx" > /dev/null; then
        echo "RTSP-server STARTED!"
    else
        echo "RTSP-server NOT STARTED"

        cd /home/user/Mediamtx
        MTX_RTSPADDRESS=":${a_pRTSP}" MTX_RTMPADDRESS=":${a_pRTMP}" MTX_PROTOCOLS="tcp,udp" ./mediamtx &
    fi

    sleep 2
done
~~~

## Video-server
 _&ensp;&nbsp;*used third-party software_<br>
 
### Functions
Publishing and broadcasting a video stream of a desktop.

### Exemple
- <a href="https://github.com/bluenviron/mediamtx/tree/main" target="_blank">mediamtx</a> - RTSP, RTMP and other protocols available;
- <a href="https://www.digitalocean.com/community/tutorials/how-to-set-up-a-video-streaming-server-using-nginx-rtmp-on-ubuntu-20-04" target="_blank">Nginx-RTMP</a> - RTMP protocol available;
- or other RTSP, RTMP server;

### Features
- if you are not using desktop capture/broadcast, then installing a **Video-server** is not required.

## License
All code in this repository is released under the <a href="https://github.com/In-spectrum/RedCAM/blob/main/LICENSE">MIT license</a>. 
<br>Application archives and compiled binaries make use of some third-party dependencies:
- Qt - the primary <a href="https://www.qt.io/licensing/open-source-lgpl-obligations#" target="_blank">open-source license</a> is the GNU Lesser General Public License v.3 <a href="https://www.gnu.org/licenses/lgpl-3.0.txt" target="_blank">“LGPL v3”</a>;
- GStreamer - <a href="https://github.com/GStreamer/gstreamer/blob/main/LICENSE" target="_blank">licensed under the LGPL v2.1;
