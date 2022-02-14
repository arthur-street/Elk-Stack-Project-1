# Elk-Stack-Project-1
This project's purpose is to show knowledge in creating, configuring and launching a virtual network using Elk Stack

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Red Team Network Diagram](https://github.com/arthur-street/Elk-Stack-Project-1/blob/main/Diagrams/Screenshot%202022-02-12%20212253.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Red Team Network Diagram file may be used to install only certain pieces of it, such as Filebeat.

  - https://github.com/arthur-street/Elk-Stack-Project-1/blob/main/Ansible/filebeat-playbook.yml.txt
  - https://github.com/arthur-street/Elk-Stack-Project-1/blob/main/Linux/filebeat.cfg.txt 

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly functional, in addition to restricting high-traffic to the network.

- What aspect of security do load balancers protect?
  - Keeps the servers from overloading and allows for maximum use.
  - allows server to throw off potential attacks (DDOS) 

- What is the advantage of a jump box?_
  - they are able to hold at bay any potential threats by containing it to a non admin used space, separate from the potential targets within the server.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the Network and system logs.

- What does Filebeat watch for?_
  - It monitors the log files/locations that you specify and forwards them to Elasticsearch/Logstash for indexing.

- What does Metricbeat record?_
  - it records metric/stats data and transports them to the output through Elasticsearch/Logstash

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Elk-vm   | Server   |40.77.49.101| Linux            |
| Web-1    | Server   | 10.0.0.5   | Linux            |
| Web-2    | Server   | 10.0.0.6   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 73.147.142.25

Machines within the network can only be accessed by Jump box Provisioner.
- Which machine did you allow to access your ELK VM? 
  - Jump box Provisioner

- What was its IP address?_
  - 10.0.0.4



A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 73.147.142.25        |
| ELK-VM   | no                  | 10.0.0.4             |
| Web-1    | no                  | 10.0.0.4             |
|  Web-2   | no                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?
  - One main advantage would be YAML Playbooks. It is the best alternative for configuration management/automation.
  - It is also able to automate complex multi-tier IT application environments. 

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._

- First I, SSH into the Jump-Box-Provisioner (ssh redadmin@52.170.85.151)
	- Start/Attached to the ansible docker (sudo docker start bold_raman)/(sudo docker attach bold_raman)
	- Went to /etc/ansible/roles directory and created the ELK playbook (elk-playbook.yml)
	- Ran the elk-playbook.yml in that same directory (ansible-playbook elk-playbook.yml)
	- Lastly, I SSH into the ELK-VM to verify the server is up and running.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Elk-VM Docker PS]( https://github.com/arthur-street/Elk-Stack-Project-1/blob/main/Images/Screenshot%202022-02-13%20142929.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- List the IP addresses of the machines you are monitoring
  - Web-1 (10.0.0.5)
  - Web-2 (10.0.0.6)

We have installed the following Beats on these machines:

- https://github.com/arthur-street/Elk-Stack-Project-1/blob/main/Images/Screenshot%202022-02-05%20202629.png
- https://github.com/arthur-street/Elk-Stack-Project-1/blob/main/Images/Screenshot%202022-02-06%20205022.png

These Beats allow us to collect the following information from each machine:
- In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc. - Filebeat is used to collect log files from specific files on remote machines.
	
  - Examples of Filebeats can be files that are generated by Apache, Microsoft Azure tools, the Nginx web server, and MySQl databases.	

	- Metricbeat collects machine metrics.
	- It is simply a measurement to tell analysts how healthy it is.
	- Examples of Metricbeat can be CPU usage/Uptime



### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/files.
- Update the filebeat-config.yml file to include...
- Run the playbook, and navigate to http:// http://40.77.49.101:5601/ to check that the installation worked as expected.

-	Complete same steps for metricbeat-config.yml


## Answer the following questions to fill in the blanks:_
- _Which file is the playbook? 

- Where do you copy it? Filebeat-playbook.yml

- _Which file do you update to make Ansible run the playbook on a specific machine? /etc/ansible

- How do I specify which machine to install the ELK server on versus which to install Filebeat on? _I have to specify two separate groups in the etc/ansible/hosts file. One of the groups will be webservers which has the IPs of the VMs that I will install Filebeat to. The other group is named elkservers which will have the IP of the VM I will install ELK to.

- _Which URL do you navigate to in order to check that the ELK server is running? http://40.77.49.101:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
