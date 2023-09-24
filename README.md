# Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Cloud Virtualization Diagram](https://github.com/jewelthomaswilliams1/Elk_Stack_Project/tree/main/Diagram)


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
			
		2. Metricbeat collects metric data from the target servers and systems. Metricbeat is part of the Elastic Stack,
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



# The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.

![docker ps successful result screenshot](https://github.com/jewelthomaswilliams1/Elk_Stack_Project/blob/main/Diagram/Docker%20PS%20screenchot%20Elk%20Installation.png)

### Target Machines & Beats

This ELK server is configured to monitor the following machines:

|DVWA1    	| 10.0.0.5     
|DVWA2          | 10.0.0.6


## We have installed the following Beats on these machines:

 # I have succesfully installed  

[Filebeat Playbook Yaml](https://github.com/jewelthomaswilliams1/Elk_Stack_Project/blob/main/Ansible/filebeat-playbook.yml)
[Metricbeat Playbook Yaml](https://github.com/jewelthomaswilliams1/Elk_Stack_Project/blob/main/Ansible/metricbeat-playbook.yml)

	 - filebeat
	 - metricbeat

These Beats allow us to collect the following information from each machine:

	-filebeat: Logs
	 	I expect to see: linux logs information. This allows us to track things like user logon events, failed access attempts, service starts and stops
	-metricbeat: metrics and system statistics
		I expect to see: from the linux metric and system statistics gathered cpu usage, memory usage, drive space usage and drive space available for each 
		of my target machines


### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible.cfg file to /etc/ansible.
		
- Update the host file to include the specific machine in which Ansible should run the playbook as opposed to where the ELK server should be installed on.
- Run the playbook, and navigate to your elk server using port 5601 to check that the installation worked as expected. 
- 
	Verify that you can access your server by navigating to http://[my.ELK-VM.External.IP]:5601/app/kibana. 
	Using the public IP address of my new ELK VM
## the result should look like this
![Kibana Success screenshot](https://github.com/jewelthomaswilliams1/Elk_Stack_Project/blob/main/Diagram/Kibana%20success%20config.png)
![Kibana Success screenshot 2](https://github.com/jewelthomaswilliams1/Elk_Stack_Project/blob/main/Diagram/Kibana%20successful%20configuration.png)
	


