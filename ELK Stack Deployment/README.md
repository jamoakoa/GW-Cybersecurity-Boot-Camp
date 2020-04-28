The files in this repository were used to configure the network display below:

![]()

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the main.yml file may be used to install only certain pieces of it, such as DVWA.

    install-dvwa.yml

This document contains the following details:

   * Description of the Topology
   
   * Access Policies
   
   * ELK Configuration
   
   * Beats in Use
   
   * Machines Being Monitored
   
   * How to Use the Ansible Build

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

Name | Publicly Accessible | Allowed IP Addresses
---- | ------------------- | ---------------------
Jump Box | No | Confidential (Local Network IP)
DVWA-VM1 | No |	Confidential (Local Network IP)
DVWA-VM2 | No |	COnfidential (Local Network IP)
ELK Server | No | Confidential (Local Network IP)

Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it increases accuracy, be eliminating human error in retyping commands and saves time.

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

The following screenshots display the result of running docker ps after successfully configuring the ELK instance.
Target Machines & Beats

This ELK server is configured to monitor the following machines:

    10.2.0.5
    10.2.0.6

We have installed the following Beats on these machines:

    * filebeat
    * metricbeat
    
These Beats allow us to collect the following information from each machine:

* Filebeat allows for a lightweight way to forward and centralize logs and files. This provides a GUI and infographic view in order to track down curious behavior across aggregated logs.
* Metricbeat allows for a lightweight way to send system and service statistics. This provides a GUI and infographic view of system-level CPU usage, memory, file system, disk IO, network IO statistics, and top-like statistics for every process running on your systems.

<Using the Playbook>

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:

ssh -i <key_name/location> <username>@<Jump-Box-Public-IP>
sudo docker start <container_name>
sudo docker attach <container_name>

    Copy the entire roles folder, including subfolders and files to /etc/ansible/roles/.
    Update the host file to include the IP addresses for the webservers and the elkserver.
    Update each configuration file with the following information:
        kibana host (uncomment and replace localhost with your local IP for your ELK server)
        elastic.search output (uncomment and replace localhost with your local IP for your ELK server)
    Run the playbook, and navigate to http://<Elk-Server-Public-IP>:5601 to check that the installation worked as expected.

ansible-playbook /etc/ansible/main.yml
