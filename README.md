## Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.

![diagram](Diagrams/Cloud_Diagram.png.png?raw=true)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the ansible playbook file may be used to install only certain pieces of it, such as Filebeat.
--
\---

\- name: installing and launching filebeat

  hosts: webservers
  
  become: yes
  
  tasks:
  
\- name: download filebeat deb

  command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-amd64.deb 
  
\- name: install filebeat deb

  command: dpkg -i filebeat-7.6.1-amd64.deb

\- name: drop in filebeat.yml 

  copy:
  
    src: /etc/ansible/files/filebeat-config.yml
    
    dest: /etc/filebeat/filebeat.yml
    
\- name: enable and configure system module

  command: filebeat modules enable system
  
\- name: setup filebeat

  command: filebeat setup
  
\- name: start filebeat service

  command: service filebeat start
  
\- name: enable service filebeat on boot

  systemd:
  
    name: filebeat
    
    enabled: yes
    
\---
--
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application. Load balancing ensures that the application will have high availability, in addition to restricting traffic to the network. Load Balancer secures the availability aspect of security, prevents failure caused by overloading a particular resource through even distribution of network traffic. Further, by shifting attack traffic from the corporate server to a public cloud provider it will deflect distributed denial of service (DDoS) attacks. The advantage of jump box is easy securement and monitoring of traffic because it forces all network traffic  through only a single node. An ELK server is included because it allows users to monitor the vulnerable VMs for changes to the file and system logs. Within the ELK server there are installed beats tools like Filebeat, to monitor log files, collect log events, and send them either to Elasticsearch or Logtash for indexing; while metricbeats collect server’s metrics and statistics and send those outputs to either Elasticsearch or Logtash as well. 

The configuration details of each machine may be found below.

|  Name      |  Function    | IP Address      |  Operating System  |
|------------|--------------|-----------------|--------------------|
|  Jump Box  |  Gateway     |  20.92.77.134   |  Linux             |
|  Web-1     |  Web server  |  10.1.0.7       |  Linux             |
|  Web-2     |  Web server  |  10.1.0.8       |  Linux             |
|  Web-3     |  Web server  |  10.1.0.9       |  Linux             |
|  elk-VM    |  ELK server  |  13.88.223.7    |  Linux             |

### Access Policies
The machines on the internal network are not exposed to the public Internet. Only the elk-VM machine and the load balancer can accept connections from the Internet. Access to these machine is only allowed from the following IP addresses:
	- 99.253.224.70 

Machines within the network can only be accessed by local host computer.
The machines, that can access ELK VM, are host computer with external IP address 99.253.224.70, and Ansible machine through ssh, with IP address 10.1.0.4. 

A summary of the access policies in place can be found in the table below.

|Name   |Publicly Accessible   | Allowed IP Address                    |
|-------|----------------------|---------------------------------------|
|jumpbox|yes(ssh)              | 99.253.224.70, Virtual Network’s IPs    |
|Web-1  |no                    | 10.1.0.4, 10.0.0.8, 20.213.89.69      |
|Web-2  |no                    | 10.1.0.4, 10.0.0.8, 20.213.89.69      |
|Web-3  |no                    | 10.1.0.4, 10.0.0.8, 20.213.89.69      |
|elk-VM |yes                   |99.253.224.70, Virtual Network’s IPs   |

### Elk Configuration
 
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it leads to more productivity, saving time, eliminating repetitive tasks, leading to less errors, and increasing accountability and compliance.

The playbook implements the following tasks:
- install docker and python3 engine  
- increase the virtual memory
- download sebp/elk:740 image container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![images](images/docker_ps_output.png?raw=true)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.1.0.7 Web-1	
- 10.1.0.8 Web-2	
- 10.1.0.9 Web-3

We have installed the following Beats on these machines:
- filebeat-7.6.1-amd64.deb
- metricbeat-7.6.1-amd64.deb

These Beats allow us to collect the following information from each machine:
- Filebeat is collecting Log files/machine data, that we use for security and surveillance, tracking a full history of events over time.
- Metricbeat takes the metrics and statistics, which we use to monitor the web servers' health (CPU usage, memory, file system, disk, and network).

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
SSH into the control node and follow the steps below:
- Copy the YAML playbook file to /etc/ansible directory.
- Update the ansible host file to include private IP address with ansible python interpreter next to it (webserver group and elk group).
- Edit the ansible configuration's remote_user with admin username for ssh connections. 
- Run the playbook, and navigate to docker web machines to check that the installation worked by ssh or curl command.
- To verify the elk installation open the web page and navigate to http://<ELK_VM_EXTERNAL_IP>:5601/app/kibana



