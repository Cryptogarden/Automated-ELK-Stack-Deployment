## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/Cryptogarden/Automated-ELK-Stack-Deployment/blob/main/Network%20Diagram.jpg

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

- elk_stack-playbook.yml (https://github.com/Cryptogarden/Automated-ELK-Stack-Deployment/blob/main/docker%20setup-playbook.yml)

- docker setup-playbook.yml (https://github.com/Cryptogarden/Automated-ELK-Stack-Deployment/blob/main/docker%20setup-playbook.yml)

- filebeat-playbook.yml (https://github.com/Cryptogarden/Automated-ELK-Stack-Deployment/blob/main/filebeat-playbook.yml)

- metricbeat-playbook.yml (https://github.com/Cryptogarden/Automated-ELK-Stack-Deployment/blob/main/metricbeat-playbook.yml)

 
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.
- The load balancer provides redundancy, helping to prevent any downtime. The advantage of using a jump box is to prevent and connections with the internet facing side of the network and provides an extra layer of security.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of VMs on the network and system metrics.
- Filebeat is used to detect changes to the filesystem by collecting Apache logs.
- Metricbeat is used to changes in system metrics such as CPU usage.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| DVWA 1   |Web Server| 10.0.0.5   | Linux            |
| DVWA 2   |Web Server| 10.0.0.6   | Linux            |
| ELK      |Monitoring| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 10.0.0.5,10.0.0.6

Machines within the network can only be accessed by Jump Box.
In this configuration only the DVWA 1 and DVWA 2 (10.0.0.5,10.0.0.6) machines had access to the ELK VM.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | Nat IP for Admin     |
| ELK      | No                  | 10.1.0.4             |
| DVWA 1   | No                  | 10.0.0.5             |
| DVWA 2   | No                  | 10.0.0.6             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it requires less time and resources, it ensures each deployment is the same and compatible, and it can help to avoid errors in syntax or other issues.

The playbook implements the following tasks:
- Install docker
- Install python
- Install docker python module
- Download and launch a docker elk container

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- DVWA 1/10.0.0.5
- DVWA 2/10.0.0.6

I have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat is used to detect changes to the filesystem by collecting Apache logs.
- Metricbeat detects changes in system metrics such as CPU usage. It can be used to detect failed login attempts or sudo escalations, as well as CPU/RAM statistics.

### Using the Playbook
To use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to Ansible control node.
- Update the hosts file to include hosts and targets.
- Run the playbook and navigate to http://10.1.0.4:5601 to check that the installation worked as expected.

The playbook to setup the network and deploy the Elk server is “elk_stack-playbook.yml”. It should be copied to the home/etc/ansible folder.
- To make Ansible run the playbook on a different machine, edit the config.yml file in the /home/etc/ansible directory. You will specify which machine to install a specified playbook to by providing the IP addresses for each machine in the Ansible config.yml file.
- To ensure the playbook was successfully deployed on a machine, this can be verified by navigating to http://<*new elk stack VMs IP*>:5601
