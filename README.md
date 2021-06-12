# ELK-Project

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://user-images.githubusercontent.com/79546857/121618945-526ac480-ca2d-11eb-9f9c-0381d6f74aa4.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

![image](https://user-images.githubusercontent.com/79546857/121619258-ee94cb80-ca2d-11eb-9982-dadc745a9c48.png)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network. The Load balancer encures that work to process incoming traffic will be shared by both vulnerable web servers. Accerss controls will ensure that only authorized users will be able to connect. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system of the VMs on the network and system metrics.
- Filebeat: Files beat detects changes tot he filesystem. Specifically, we use it to collect Apache logs.
- Metricbeat: Metricbeat detects changes in system metrics, such as CPU usage. We use it to detect SSH login attamps, failed sudo escalations, and CPU/RAM statistics. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.7/20.85.240.157  | Linux |
| Web-1    | Web Server | 10.0.0.5   | Linux       |
| Web-2    | Web Server | 10.0.0.6   | Linux       |
| ELK      | Monitoring | 10.2.0.4   | Linux       |

### Access Policies
a
The machines on the internal network are not exposed to the public Internet. 

Only the HOST machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 10.0.0.7/20.85.240.157
- 10.0.0.5
- 10.0.0.6
- 10.2.0.4
- 136.49.49.225
Machines within the network can only be accessed by 136.49.49.225.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 10.0.0.5/10.0.0.6    |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-Ansible allows an individual to model complex IT workflows with flexiblity and be able to be utilized in multple application enviornments with ease.  

The playbook implements the following tasks:
- Install docker.io
- Install python3-pip
- Install Docker module
- Increase virtual memory
- Download and launch a docker elk container
- Enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://user-images.githubusercontent.com/79546857/121783542-d24f7680-cb74-11eb-9767-a3900550e127.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat

These Beats allow us to collect the following information from each machine:
-Filebeat can be used to collet, parse, and visualize ELK logs in a single command. By taking raw log files, Kibana projects the Filebeat data from both virtual machines in order to monitor them. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- SSH into Jump-Box (ssh RedAdmin@20.85.240.157)
- Run sudo docker container list -a
- Run sudo docker container start priceless_diffie
- Run sudo docker container attach priceless_diffie (root@714b61654e17)
- Cd into /etc/ansible*
- Copy the filebeat-config.yml file to files. (after edits)
- Update the host file to include the ELK machine as well as 10.0.0.5 and 10.0.0.6
- Run the playbook, and navigate to Kibana (with the correct corresponging IP address) to check that the installation worked as expected.


