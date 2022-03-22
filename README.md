## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt text](https://github.com/DH7777/Cyber-Project1/blob/main/Diagrams/Diagram_network.png "Diagram_network")

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ELK_install_playbook file may be used to install only certain pieces of it, such as Filebeat.

[ELK_install_playbook](https://github.com/DH7777/Cyber-Project1/blob/main/Ansible/ELK_install_playbook)

[Filebeat_install_playbook](https://github.com/DH7777/Cyber-Project1/blob/main/Ansible/Filebeat_playbook)

[Metricbeat install playbook](Ansible/Metricbeat_install_playbook)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting unwanted access to the network.

-Load Balancers will help distribute incoming requests so that one server will not get overwhelmed and cause it to shut down.  Having it set up this way, will also help against DDOS attacks that would render a server useless, but with a load balancer, the next server would be able to carry the load until you can get the attacked server back up. Creating a JumpBox also eliminates the security risk of the servers data being able to get hacked, since the attackers won’t be able to get to the servers themselves.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems and watch system metrics.

-Filebeat is a shipper for forwarding and centralizing logdata.  It will monitor the log files and collect log events, and forwards them to Elasticsearch for indexing. 

-Metricbeat would record the operational state of the computer and send them to Elasticsearch.  It can be helpful in determining uptime, CPU usage , and other info needed for upgrades.

The configuration details of each machine may be found below.


| **Name**   | **Function** | **IP Address** | **Operating System** |
|------------|--------------|----------------|----------------------|
| Jump-Box   | Gateway      | 10.1.0.4       | Linux                |
| Web-1      | Server       | 10.1.0.5       | Linux                |
| Web-2      | Server       | 10.1.0.6       | Linux                |
| ELK-Server | Monitoring   | 10.2.0.4       | Linux                |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

76.30.62.136

Machines within the network can only be accessed by Jump-Box.

The ELK server can be accessed only by the Jump-Box with IP 10.1.0.4

A summary of the access policies in place can be found in the table below.

| **Name**   | **Publicly Accessible** | **Allowed IP Addresses** |
|------------|-------------------------|--------------------------|
| Jump-Box   | Yes                     | 76.30.62.163             |
| Web-1      | No                      | 10.1.0.4                 |
| Web-2      | No                      | 10.1.0.4                 |
| ELK-Server | No                      | 10.1.0.4                 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
If we ever need to add more VMs, we can implement the same settings to all of them at once, instead of doing it one by one.

The playbook implements the following tasks:

 - Installs Docker
 - Installs Python-pip
 - Installs Docker python Module
 - Increases virtual memory
 - Downloads and launches a docker ELK container with the ports 5601, 9200, 5044

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![alt text](https://github.com/DH7777/Cyber-Project1/blob/main/Diagrams/ps%20docker.png "Docker_screenshot")


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
| **Name** | **IP Addresses** |
|----------|------------------|
| Web-1    | 10.1.0.4         |
| Web-2    | 10.1.0.4         |


We have installed the following Beats on these machines:

ELK-Server: Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
Filebeat- Collects data about the file system which can be helpful when looking for which file system was accessed.
Metricbeat - Collects data about the health of the machines to determine what machines need to be upgraded or looked at.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible.
- Update the hosts file to include ELK-server 10.2.0.4
- Run the playbook, and navigate to the public ip of the ELK-Server(ip address:5601) to check that the installation worked as expected.

The playbook is install-elk.yml located in /etc/ansible
You would have to update the hosts file in /etc/ansible and by adding a different IP, you can make it run on a specific machine.
The URL would be the (IP address of the VM:5601)



