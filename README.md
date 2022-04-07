## Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.

![diagram](C:\Users\jeffp\Documents\resources\Project-1\Project\README\Images\Cloud_Diagram.png.png?raw=true)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the ansible playbook file may be used to install only certain pieces of it, such as Filebeat.

\---
- name: installing and launching filebeat
  hosts: webservers
  become: yes
  tasks:
- name: download filebeat deb
  command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-amd64.deb 
- name: install filebeat deb
  command: dpkg -i filebeat-7.6.1-amd64.deb
- name: drop in filebeat.yml 
  copy:
    src: /etc/ansible/files/filebeat-config.yml
    dest: /etc/filebeat/filebeat.yml
- name: enable and configure system module
  command: filebeat modules enable system
- name: setup filebeat
  command: filebeat setup
- name: start filebeat service
  command: service filebeat start
- name: enable service filebeat on boot
  systemd:
    name: filebeat
    enabled: yes
\---
