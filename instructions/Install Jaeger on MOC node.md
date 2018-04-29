Thanks to 

Bowen Song and Ceph tracing team.

This document is donated by them.

1 Introduction

This document is to illustrate an example of how to setup Jaeger on Centos in MOC. The setup involves 2 VMs, VM6 and VM7. Setup would involve Jaeger and Docker on both VMs.
To demonstrate an understanding, I am deploying HOTRod on the VMs. Front end of HOTRod would be on VM6 and All other components would be on VM7.
This would demonstrate my understating of HOTRod and Jaeger in the attempt to trace HOTRod application.

2 SSH Into VMswith respect to current configuration

	ssh -A -i centos@128.31.26.26 
	ssh centos@192.168.0.17 

3 Show Docker Jaeger GUI
	
We use X11 the show Jaeger GUI on local computer.

 Setup X11 on local Computer

 Changes to /etc/ssh/sshd_config should be:
	
	AllowAgentForwarding yes 
	X11Forwarding yes

 Install X11 

	sudo yum install xorg-x11-xauth xterm

 Allow sshd.service

	systemctl enable sshd.service

 Restart sshd.service for ssh_config to work:

	systemctl restart sshd.service

 Install Firefox to see GUI

	sudo yum install firefox

 Allow display

	sudo yum groupinstall GNOME Desktop

 Install X11

	sudo yum groupinstall 'X Window System'

 x11 authentication

	sudo yum install xorg-x11-xauth

	sudo yum search xorg-x11

	sudo vim .bashrc 
 	
 and add “export DIS- PLAY=localhost:10.0”

The .bash profile should look like

	# .bash_profile
	# Get the aliases and functions
	if [ -f ~/. bashrc ]; then 
			. ~/. bashrc
	PATH=$PATH:$HOME/.local/bin:$HOME/bin:
	export PATH
	export GOBIN="$HOME/projects/bin" 
	export GOPATH="$HOME/projects/src"