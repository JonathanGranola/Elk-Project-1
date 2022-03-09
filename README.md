# Elk-Project-1
Jonathan Gurrola Elk-Repo
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![This is an image](https://user-images.githubusercontent.com/90113483/156936776-0b93bb32-018c-461b-a604-dfd4ccf0339f.PNG)
(https://docs.google.com/document/d/1jxIFQI0hJVFvi5wgVWvqTesbPRe0TJtmYn9Xunth2Ts/edit)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


## Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly availabl, efficient and reliable, in addition to restricting access to the network.

What aspect of security do load balancers protect? What is the advantage of a jump box?

The off-loading function of a load balancer defends an organization against distributed denial-of-service (DDoS) attacks. It does this by shifting attack traffic from the corporate server to a public cloud provider. (Source: https://avinetworks.com/what-is-load-balancing/). The load balancer, as the name implies, insures that the work to process incoming traffic is shared by all load balanced servers.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of the ervers on the network, and system metrics such as CPU usage, steempted SSH logins, sudo escalation failures, ect.

- Filebeats watch for changes to the file system. Specifically, we use it to collect Apache logs. The Apache HTTP Server provides very comprehensive and flexible logging capabilities. Apache httpd is capable of writing error and access log files through a pipe to another process, rather than directly to a file. This dramatically increases the flexibility of logging, without adding code to the main server. (Source: https://httpd.apache.org/docs/2.4/logs.html ) - Piped Logs.

- Metricbeats record and monitor statistics from the running servers to help identify changes in system measurements. Data retrieved can include operating system metrics such as CPU or memory usage, or data related to services running on the server(s).

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name      | Function        | IP Address | Operating System |
|-----------|-----------------|------------|------------------|
| Jump Box  | Gateway         | 10.0.0.1   | Linux            |
| Web-1     | WebServer       | 10.0.0.5   | Linux            |
| Web-2     | WebServer       | 10.0.0.6   | Linux            |
| Elk-Server| MonitoringServer| 10.1.0.4   | Linux            |

## Access Policies

The machines on the internal network are not exposed to the public Internet. 

### Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 68.203.13.109 (my local host public IP address, IPV4)

### Machines within the network can only be accessed by eachother.
- I allowed the Jump-box to access my ELK VM. The IP address used: 10.0.0.7

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses |
|-----------|---------------------|----------------------|
| Jump Box  | Yes                 | 10.0.0.7             |
| Web-1     | No                  | 10.0.0.5             |
| Web-2     | No                  | 10.0.0.6             |
| Elk-Server| No                  | 10.1.0.4             |


## Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- it avoids human error. Using automation allows for much greater scaling and reduces administrative burden.

- Another great advantage of automating the configurations for Ansible is that it allows an administrator to deploy multiple servers with a single YAML playbook with minimal changes.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Elk](https://user-images.githubusercontent.com/90113483/157352236-108e179d-e1f0-449b-90a2-adc8898a3e16.jpg)

This playbook implements the following tasks as indicated in the elk.yml file:

- Configure Elk VM with Docker
- Install docker.io
- Install pip3
- Install Docker python module
- Download and launch a docker elk container

The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.

![Capture](https://user-images.githubusercontent.com/90113483/157354227-f01e8a85-479e-4a60-b17d-615d0141ebda.PNG)

## Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 – 10.0.0.5
- Web-2 – 10.0.0.6

We have installed the following Beats on these machines:

- Filebeats is a log message provider. Its principle of operation is to monitor and collect log messages from log files and send them to Elasticsearch or LogStash for indexing. Examples of what I would expect to see is information logged on SSH logins and sudo commands.

- Metricbeats (not installed on my system) – collects metrics that developers can use with the Kibana dashboard to visualize the information received.


## Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to /etc/ansible (cd /etc/ansible) The /etc/ansible directory contains the files: ansible.cfg, elk.yml, and hosts.
- Update the hosts file to include ip addresses for webservers (Web-1 & Web-2) as well as the ELK virtual machine.
- Run the playbook, and navigate to Kibana dashboard to check that the installation worked as expected.

- _Which file is the playbook? The playbook is a YAML file (extension .yml).                                                    
- _Which file do you update to make Ansible run the playbook on a specific machine? Host
- _Which URL do you navigate to in order to check that the ELK server is running? When the ELK machine is up and running, use the curl command or open a new browser and use the public ip address & port 5601 for the ELK machine (20.110.123.43).
   -        http://[ **20.110.123.43**]:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.
- the #### nano camand to edit and update the yaml files.
