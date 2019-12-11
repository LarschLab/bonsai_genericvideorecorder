# bonsai_genericVideoRecorder

Barebone video recorder workflow using Bonsai &amp; ffmpeg.

Strength: very fast real time video compression on modest hardware using any DirectShow Camera.  Extend with live tracking etc. using Bonsai environment.


The workflow implements the following strategy:

video acquisition - pipe frames to ffmpeg - start ffmpeg process to receive and compress frames.


----------------------
Setup:
----------------------

Install bonsai
https://bonsai-rx.org/
 
download and unzip ffmpeg
(unzip to c:\ffmpeg\ without further subfolders to simplify things later)
https://www.ffmpeg.org/

by default, data will be stored at c:\data\
 
For details on parameters, you can check the following forum entry on bonsai and video pipe to ffmpeg:
https://groups.google.com/forum/#!msg/bonsai-users/xwqMzIbyeC4/iQJi1_4XiwEJ


----------------------
Short summary:
----------------------

Video acquisition from directShow camera

	-Depending on camera, this will use the last camera settings for fps, resolution etc.
	-Some cameras allow saving configuration files. IDS cameras can load file via Bonsai, maybe others too?

Background subtraction

	-continously updating background estimation
	-can customize parameters or remove this function entirely.

Ffmpg starts as a background process that is configured in a short python script (the node named 'ffmpeg' in the workflow).

	-supports fine configuration of video parameters.
	-here, we use 'grayscale', xVid compression
	-specify fps for correct playback and video quality to compromise file size.
	-can change data storage location and ffmpeg path in this script.


----------------------
Known issues:
----------------------

-If workflow stalls without properly closing video pipe, next time workflow plays you will get an error 'pipe is busy'.
You can manually start ffmpeg process to process the data & clear the pipe or simply close and restart bonsai.
