# Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/ganjuice/ELK-Stack/blob/main/Diagrams/Network%20Diagram.PNG

These files have been tested and used to generate a live ELK deployment an Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
 - Beats in Use
 - Machines Being Monitored
- How to Use the Ansible Build

# Description of the Topology

The main purpose of this netowrk is to expose a load-balanced and monitored instance of DVWA, the D@mn Vulnerable Web Aplication.

Load balancing ensures that the application will be highly responsive, in addition to restricting traffic to the network.
What aspect of security do load balancers protect?
Load Balancing plays an important sercurity role in cloud computing. The off-loading function of a load balancer devends an organization against distributed denial-of-service (DDoS) attacks.
What is the advantage of a jump box?
A jump box is a secure computer that all admins first connect to before launching any administrative task of use as an origination point to connect to other serviers of untrusted environments.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system configuration.
What does Filebeat watch for?
Filebeat is a lightwweight shipper for forwarding and centralizing log data. It monitors the log files of locations taht you specify, collects log events, and forwards them either to Elastic search of Logstash for indexing.
What does Metricbeat record?
Metricbeat is a lightweight shiper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch of Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web-1    | DVWA     | 10.0.0.5   | Linux            |
| Web-2    | DVWA     | 10.0.0.6   | Linux            |
| ELK      |Web Server| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Add whitelisted IP addresses
(MY persal IP address IPv4)

Machines within the network can only be accessed by Jump Box.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
I allowed Jump Box access only from IP address 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses          |
|----------|---------------------|-------------------------------|
| Jump Box | No                  |(MY persal IP address IPv4)    |
|          |                     |                               |
|          |                     |                               |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
When multiple machines need to be configured automation reducces human error and increases efficiency.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Install docker.io
- Install python3-pip (takes care of conflicts bewten python versions 2 and 3)
- Install Python Docker module
- Use command module to increase virtual memory
- Use sysctl module to use the virtual emmory that was added above
- Use docker_container module to download and launch a Docker ELK container on a server

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
Web-1 10.0.0.5
Web-2 10.0.0.6

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
filebeats
metricbeats

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the .yml (playbook) file to Ansible.
- Update the hosts file to include the slave server.
- Run the playbook, and navigate to target (slave server) to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
elk.yml vigorous_moser (name of Ansible container)
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
update the hosts file. And give target instructions in "hosts:" section of playbook
- _Which URL do you navigate to in order to check that the ELK server is running?
<IPaddress>:5601/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
