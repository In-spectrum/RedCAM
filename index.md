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
  * [Properties](#properties)
  * [Install](#install)
* [**RedCAM-client**](#RedCAM-client)
  * [Functions](#functions-1)
* [**License**](#license)

## **RedCAM-server**
### Functions  
  &emsp;&nbsp;- user registration;
  <br>&emsp;&nbsp;- recording video files;
  <br>&emsp;&nbsp;- user access to cameras and files (depending on the status);

### Properties
**-pas** - set server password (default 1111); _**./RedCAMServer.sh -pas 2227**_<br>
**-p** - set listen port; _**./RedCAMServer.sh -p 1675**_<br>
**-prtsp** - set port for viewing video files; _**./RedCAMServer.sh -prtsp 8654**_<br>

### Install
 - download <a href="https://github.com/In-spectrum/RedCAM/releases" target="_blank">application archive</a> and unzip;
 - start the server with parameters: **_RedCAMServer -pas 2227 -p 1675 -prtsp 8654_**

## RedCAM-client
The administrator creates users and has access to all cameras.

### Functions
- adding/deleting RTSP streams of its cameras;
- simultaneous viewing of several video cameras;
- setting the total time for recording files;
- setting the status of the video camera as publicly available for all users on the server;
- generating code for viewing the video camera by clients who are not connected to the server but have the application installed.
   
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
