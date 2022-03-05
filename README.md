## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - DVWA
  - Filebeat
  - Metricbeat
  - ELK Stack

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

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes made to them on the network and gather system metrics.  In the ELK stack we are using Filebeat for the centralization and forwarding of data.  Filebeat monitors and collects log events, which ever you specify, and sends them to Elasticsearch/logstash.

The configuration details of each machine may be found below.

| Name                       | Function       | IP Address | Operating System |
|----------------------------|----------------|------------|------------------|
| Jump-Box-Provisioner       | Gateway        | 10.0.0.5   | Linux            |
| Web-1 (DVWA 1)             | Web Server     | 10.0.0.9   | Linux            |
| Web-2 (DVWA 2)             | Web Server     | 10.0.0.10  | Linux            |
| ELK                        | Monitoring     | 10.1.0.4   | Linux            |

### ELK Server Configuration

The ELK VM exposes an Elastic Stack instance. Docker is used to download and manage an ELK container.

Rather than configure ELK manually, we opted to develop a reusable Ansible Playbook to accomplish the task. This playbook is duplicated below.

To use this playbook, one must log into the Jump Box, then issue: ansible-playbook install_elk.yml elk. This runs the install_elk.yml playbook on the elk host.


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the public facing machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My person ip (24.x.x.x)

Machines within the network can only be accessed by each other. The DVWA 1 and DVWA 2 VMs send traffic to the ELK server.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 |  my personal ip      |
|  ELK     |    No               |    10.0.0.5          |
|  DVWA1   |    No               |    10.0.0.5          |
|  DVWA1   |    No               |    10.0.0.5          |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it avoids human error and increases the scalability of your petwork

The playbook implements the following tasks:
- 1: Downloads and installs Docker
- 2: Installs python and the python docker module
- 3: Allows our ELK Server VM to increase the RAM as needed for better functionality
- 4: Downloads, installs and starts ELK on a docker containter within the ELK Server
- 5: Docker services enable on the boot of the ELK VM

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Alt text](/Screenshots/elkvmdockerps.PNG?raw=true)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 (DVWA1) 10.0.0.9
- Web-2 (DVWA2) 10.0.0.10

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:

- Filebeat: Filebeat is being used to collect log file data that is sent to Elasticsearch and Logstash.  
- Metricbeat: Metricbeat collects and sends metric data on specified services.  This can provide information on memory and data usage.  


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ELK (what) file to /etc/ansible.
- Update the hosts file to include your webserver private IPs and elk IP.  Also include "ansible_python_interpreter=/user/bin/python3" to use python as the interpreting language.
- Run the playbook, and navigate to the ELK Server's IP address to check that the installation worked as expected.

![Alt text](/Screenshots/elkkibanaweb.PNG?raw=true)

- Run the playbook by using 'ansible-playbook install-elk.yml' located in '/etc/ansible/hosts/ directory
- We updated the hosts file in order to let Ansible know which specific machine to install the ELK server to vs Filebeat and Metricbeat.
- _Which URL do you navigate to in order to check that the ELK server is running?
- Navigate to 'http://<ELK-Server-Public-IP>:5601/app/kibana

