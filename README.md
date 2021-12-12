## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

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

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_

Load balancers The load balancer can help prevent a DDoS attack.  A Jump Box prevents all Azure VM's being exposed publicly.  The jump box is a gateway to the subnetworks with only a single point of entry. This allows us to easliy setup a network security group to restrict the IP addresses able to communicate with the Jumpbox/subnets.  

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes made to them on the network and gather system metrics.  In the ELK stack we are using Filebeat for the centralization and forwarding of data.  Filebeat monitors and collects log events, which ever you specify, and sends them to Elasticsearch/logstash.
- _TODO: What does Filebeat watch for?_  
- _TODO: What does Metricbeat record?_

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Webset1     | Webserver |            | Linux            |
| Webset2     |   Web Server |            | Linux            |
| ELK     |    Monitoring      |            | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump-box machine can accept connections from the Internet. Access to this machine is only allowed from my current IP address.  Which I won't publicy upload to github, but here is an example IP: 84.11.79.46.  This is the only whitelisted IP that the jump box will allow traffic to and from.  This is done by the network security group configured with the Jump box provisioner.  This NSG only allows access over port 22 for SSH access and port 3389 for RDP access. Additionaly the rules are set to allow inbound traffic over port 80 for the load balancer.

Machines within the network can only be accessed by the Jump box provisioner or other VMs on this same network.  I allowed access to my ELK VM from Web1 and Web2 VMs.  I have setup the ELK virtual machine to be accesible from Jump Box via Virutal Network Peering.  Public IP address: 20.119.48.118

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 84.11.79.46   |
|     ELK   |   no                     |                      |
|     Web1/2  |   no                  |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows for scaling with minimal effort.  

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following private IPs of the machines:
10.1.0.8
10.1.0.6

We have installed the following Beats on these machines:
Metric Beat
File Beat

These Beats allow us to collect the following information from each machine:

- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._