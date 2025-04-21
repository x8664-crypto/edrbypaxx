# Disclaimer

Content of this page must be considered as informative only and you should not attempt to replicate the behaviour outside a lab.

# EDR Tampering using eBPF on linux

SentinelOne does a pretty good job compared to the competitors to stop the tampering with its processes and daemons. Crowdstrike is years behind for instance.

Consider the scenario where you already escalated privileges in a linux box and became root. You'd like to kill the EDR agents to avoid telemetry to be sent to cloud console and avoid forensic analysis on post mortem.

In the new versions they're using eBPF technology to prevent a kill signal to be issued from root user to their daemons. In that case the shell process trying to kill the daemon will just be terminated. How's that possibile? Well, I'm not delving into details of how eBPF works, it's your task to find out info.

My idea and implementation was indeed to fight eBPF with eBPF.
The kill signal won't be launched by normal root user, but from inside a eBPF module loaded on kernel space.
You can see from this sample video that's working great by tearing down SentinelOne multiple times, till when systemd decides that enough is enough and stops restarting it. At that moment you can even uninstall SentinelOne from system.

The bzzz-edr-killer is compiled to be portable and without need of any weird dependency on system to be installed. It will just work for kernels that supports eBPF technology.

Enjoy the video.

https://github.com/user-attachments/assets/62d55910-b399-4b01-a786-325b5871286f

