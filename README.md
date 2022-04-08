# Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Cloud Virtualization Diagram](https://github.com/jewelthomaswilliams1/Elk_Stack_Project/tree/main/Diagram)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yaml and config file may be used to install only certain pieces of it, such as Filebeat.

![Ansible Playbooks and Configuration files](https://github.com/jewelthomaswilliams1/Elk_Stack_Project/tree/main/Ansible)

![Filebeat Playbook Yaml](https://github.com/jewelthomaswilliams1/Elk_Stack_Project/blob/main/Ansible/filebeat-playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
=======

Load balancing ensures that the application will be highly _accessible_, in addition to restricting _access_ to the network.

-  What aspect of security do load balancers protect? What is the advantage of a jump box?

		1. Load balancers protect availability, web traffic and web security 
		2. The advantage of a jump box is that there is Network segmentation, access control, scalable security and all of this is automated.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _data_ and system _logs_.

		1. Filebeat looks for logs; audit logs, deprecation logs, gc logs, server logs, and slow logs.  
		It then forwards that information to Elasticsearch or Logstash. 
			
		2. Metricbeat collects metric data from your target servers and systems. Metricbeat is part of the Elastic Stack,
		meaning it works seamlessly with Logstash, Elasticsearch, and Kibana. 


The configuration details of each machine may be found below.

| Name     			| Function  | IP Address		 | Operating System |
|------------------------------	|---------- |-------------------------	 |------------------|
| Jump Box 			| Gateway   | 10.0.0.4 / 20.92.105.112	 | Linux            |
| DVWA1    			| Webserver | 10.0.0.5 /20.213.34.71     | Linux            |
| DVWA2    			| Webserver | 10.0.0.6/20.213.34.71  	 | Linux            |
| ELK-VM  			| Elk Server| 10.1.0.5 /Elk-UAE-VM-ip 	 | Linux            |
| Load Balancer			|LB	    | HTTP : 80


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _local working_ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

			- my local working machine's whitelisted IP address was: 
						99.238.146.345

Machines within the network can only be accessed by ssh through ansible using TCP port 5601.

		- My local working machine  was able to access my ELK VM (via my Jumpbox's Ansible docker container) using TCP port 5601.  
	
			 Jump Box | Gateway   | 10.0.0.4  

A summary of the access policies in place can be found in the table below.



| Name     			| Function  | IP Address		 | Operating System | Publically Accessible| Allowed IP Addresses |
|------------------------------	|---------- |-------------------------	 |------------------|------------------ |-------------------------|
| Jump Box 			| Gateway   | 10.0.0.4 / 20.92.105.112	 | Linux            |N 	                |99.238.146.345 via SSH 22
| DVWA1    			| Webserver | 10.0.0.5 /20.213.34.71     | Linux            |N 	                |10.0.0.4 via SSH 22
| DVWA2    			| Webserver | 10.0.0.6/20.213.34.71  	 | Linux            |N 	                |10.0.0.4 vis SSH 22
| ELK-VM  			| Elk Server| 10.1.0.5 /Elk-UAE-VM-ip 	 | Linux            |N                  |99.238.146.345 via TCP 5601
| Load Balancer  		| LB	    |Redteam_LBR (Tcp/80)	 |		    |N			|99.238.146.345 via HTTP 80


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

	- The main advantages of automating configuration with Ansible is that it's agentless, customizable and flexible based based on specific clients' needs and does not require any further installation or other software or firewall ports on the systems that are being automated ( just a playbook). Furthermore it's very simple to set up and use and doesn't require any special coding skills.  Regardless of that fact however, it is very powerful and allows highly complex IT workflows to be set up. 


The playbook implements the following tasks:

![Elk Installation Playbook](https://github.com/jewelthomaswilliams1/Elk_Stack_Project/blob/main/Ansible/install_elk.yml)

	1) Downloads and installs Docker on the ELK server ( and use more memory otherwise the Elk container will not run)
	2) Configure it so that this setting is automatically run if your VM has been restarted.
	3) Install the following apt packages:
	
		docker.io: The Docker engine, used for running containers.

		python3-pip: Package used to install Python software.
	
	4) Install the following pip packages: 
	
		docker: Python client for Docker. Required by Ansbile to control the state of Docker containers

	5) Configure the container to start with the following port mappings:

				5601:5601, 9200:9200, 5044:5044



## h3 The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.

![docker ps successful result screenshot](https://github.com/jewelthomaswilliams1/Elk_Stack_Project/blob/main/Diagram/Docker%20PS%20screenchot%20Elk%20Installation.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

|DVWA1    	| 10.0.0.5     
|DVWA2          | 10.0.0.6

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

	I have succesfully installed  [link to ansible yml playbooks would be good here]
	filebeat
	metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

	filebeat: Logs
	metricbeat: metrics and system statistics


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
