# ELK-Project
Rice University - Project - 1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

<img src="/Diagrams/Azure Lab_ Elk Project 1.drawio.png/">

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive, in addition to restricting acess to the network.
The load balancer receives web traffic and helps distribute traffic evenly among the servers and mitgates Distributed Denial of Service (DDos) attacks across multiple servers. The load balancer also utilizes a health probe that periodically checks that a machine is working properly before sending traffic. If there is a malfuctioning machine, the load balancer will divert traffic until the issue is resolved.
The jumpbox limits the access that the public has to the virtual network and allows secured access to the virtual network and it's contents. The jump-box only allows access from IP address: 99.67.237.57 and requires a private ssh key.  


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
   Installed as an agent on the servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
  Metricbeat is installed on the different servers in the environment and used for monitoring their performance, as well as that of different external services running on them.

The configuration details of each machine may be found below.

|   Name   |           Function           |        IP Address        |    Operating System   |
|:--------:|:----------------------------:|:------------------------:|:---------------------:|
| Jump-Box |            Gateway           |  10.0.0.4 / 20.115.5.155 | Linux Ubuntu 18.04.01 |
|   Web-1  |  Webserver used to run DVWA  |         10.0.0.5         | Linux Ubuntu 18.04.01 |
|   Web-2  |  Webserver used to run DVWA  |         10.0.0.6         | Linux Ubuntu 18.04.01 |
|    Elk   | Run Elk Container and Kibana | 10.2.0.0 / 52.229.102.65 | Linux Ubuntu 18.04.01 |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 
-  99.67.237.57:22 

Machines within the network can only be accessed by the Jump-Box Provisioner VM Internal IP Address: 10.0.0.4.
The ELK VM can be accessed by the Jump-Box-Provisioner 10.0.0.4:22 and the Workstation IP 99.67.237.57:5601

A summary of the access policies in place can be found in the table below.

|      Name     | Publicly Accessible |                              Allowed IP Addresses                              |
|:-------------:|:-------------------:|:------------------------------------------------------------------------------:|
|    Jump-Box   |         Yes         |                     Workstation Public IP: 99.67.237.57:22                     |
|     Web-1     |          No         |                         Jump-Box IP: 10.0.0.4                        |
|     Web-2     |          No         |                         Jump-Box IP: 10.0.0.4                        |
| Load Balancer |         Yes         |                     Workstation Public IP: 99.67.237.57:80                     |
|      Elk      |         Yes         | Workstation Public IP: 99.67.237.57:5601 and Jump-Box Provisioner IP: 10.0.0.4:22 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it drastically reduces the potential for human error and simplifies the process of configuring multiple machines and allows for full automation of a specific server.


The playbook implements the following tasks:
- Install Docker: It will install docker.io, the docker engine that will be used for running the containers.  
- Install Python 3_pip: This will allow for additional docker modules and containers to be installed efficiantly. 
- Increase Memory/ Use More Memory: The virtual memory will need to be increased to 262144 for Elk to operate effectivley.
- Download and Launch Elk container: The Elk docker will be downloaded and launched on boot



The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines: Web -1 (10.0.0.5) and Web - 2 (10.0.0.6)

We have installed Filebeat and Metricbeat on boththe following Beats on these machines:
  Filebeat and Metricbeat 

Filebeat collects Web 1 and Web 2 system log information and specifies which files have been changed and when a file was changed to either Elasticsearch or Logstash. 
Metricbeat collects metrics and statistics form the operating system and various processes running on the servers. 
and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._                       

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/files/filebeat-config.yml.
- Update the filebeat-config.yml file to include 
- Run the playbook, and navigate to http://[your.VM.IP]:5601/app/kibana and click on "Check Data" to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook?  Filebeat-playbook.yml Where do you copy it? /etc/ansible/roles/filebeat.playbook.yml
- _Which file do you update to make Ansible run the playbook on a specific machine? filebeat-config.yml How do I specify which machine to install the ELK server on versus which to install Filebeat on? jjjjjjjjjjjjjj
- _Which URL do you navigate to in order to check that the ELK server is running? http://52.229.102.65:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
