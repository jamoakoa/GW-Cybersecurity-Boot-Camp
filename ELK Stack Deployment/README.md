The files in this repository were used to configure the network display below:

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the main.yml file may be used to install only certain pieces of it, such as DVWA.

    install-dvwa.yml

This document contains the following details:

   - Description of the Topology
    - Access Policies
    - ELK Configuration
    - Beats in Use
    - Machines Being Monitored
    - How to Use the Ansible Build

Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.

The configuration details of each machine may be found below.
Name | Function | IP Address | Operating System
---- | -------- | ---------- | ---------------- 
Jump Box | Gateway | 10.2.0.4 | Linux
DVWA-VM1 | Webserver | 10.2.0.5 | Linux
DVWA-VM2 | Webserver | 10.2.0.6 | Linux
ELK Server | Elkserver | 10.2.0.7 |	Linux

Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: redacted (home network IP)

Machines within the network can only be accessed by redacted (home network IP).

A summary of the access policies in place can be found in the table below.
Name 	Publicly Accessible 	Allowed IP Addresses
Jump Box 	No 	redacted (home network IP)
DVWA-VM1 	No 	10.0.0.5 redacted (home network IP)
DVWA-VM2 	No 	10.0.0.5 redacted (home network IP)
ELK Server 	No 	10.0.0.5 redacted (home network IP)

Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it increases accuracy, be eliminating human error in retyping commands and saves time. Roles were also utilized to increase re-usability. A main.yml file references the main.yml within each ansible role to run each playbook with one command. The main file can easily be edited to add or remove roles and therefore which playbooks are run.

The main playbook implements the following roles, which then implement the individual playbooks listed below:

    Setup Webservers
    Install Elk Server
    Install Filebeat
    Install Metricbeat

The setup-webservers playbook implements the following tasks:

    Install Docker
    Install pip
    Install Docker python module
    Download and launch docker web container

The install-elk playbook implements the following tasks:

    Install Docker
    Install pip
    Install Docker python module
    Increase virtual memory
    Download and launch docker elk container

The install-filebeat playbook implements the following tasks:

    Download filebeat .deb file
    Install filebeat
    Drop in filebeat.yml
    Enable and Configure System Module
    Setup filebeat
    Start filebeat service
