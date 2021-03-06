## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](https://github.com/JMPence89/Elk-Stack/blob/main/Nerwork_diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

my_playbook.yml

![](https://github.com/JMPence89/Elk-Stack/blob/main/Playbooks/my_playbook.yml.png)

install-elk.yml

![](https://github.com/JMPence89/Elk-Stack/blob/main/Playbooks/install-elk.yml.png)

filebeat-playbook.yml

![](https://github.com/JMPence89/Elk-Stack/blob/main/Playbooks/filebeat-playbook.yml.png)

metric-beat.yml

![](https://github.com/JMPence89/Elk-Stack/blob/main/Playbooks/metric-beat.yml.png)


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly reliable, in addition to restricting access to the network.
- The purpose of the load balancer from a security standpoint, especially as computing transitions to the cloud, is the shifting of malicious traffic from the main server. This can prevent such attacks as an imposing DDoS attack for instance.
- The Jump Box Provisioner is to give access to a single instance that can be easily monitored and secured and provide secure access to other VM's and containers.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the configuration and system files.
- Filebeat- is a lightweight container that can be easily deployed to forward and centralize log data. Filebeat monitors the log files or locations specified, collects log events, and forwards them to Elasticsearch and Logstash to be indexed.
- Metricbeat- is an add on that can monitor operating systems and service from specified VM's.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.9   | Linux            |
| Web-1    |  DVWA    | 10.0.0.7   | Linux            |
| Web-1    |  DVWA    | 10.0.0.8   | Linux            |
| ELK      |  ELK     | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 168.62.48.156

Machines within the network can only be accessed by the Jump Box Provisioner.
- Using SSH we can access Web-1 (10.0.0.7) and Web-2 (10.0.0.8)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses              |
|----------|---------------------|-----------------------------------|
| Jump Box | Yes (SSH Port 22)   |               Any                 |
|  Web-1   | No  (HTTP Port 80)  |           168.62.48.15            |
|  Web-2   | No  (HTTP Port 80)  |           168.62.48.15            |
|   ELK    | No  (HTTP Port 5601)| 168.62.48.15  10.0.0.7  10.0.0.8  |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible can be run from the command line without the use of configuration files for simple tasks to trigger updates across several VM's at once.

![](https://github.com/JMPence89/Elk-Stack/blob/main/Playbook_tasks.png)

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](https://github.com/JMPence89/Elk-Stack/blob/main/Elk_docker_run.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 	10.0.0.7
- Web-2		10.0.0.8

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

These Beats allow us to collect the following information from each machine:
- Filebeats- Collects and sends logs from Web-1 and Web-2
- Metricbeats- Collects information on operating system run-time and diagnostics on Web-1 and Web-2

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to Ansible Container.
- Update the hosts file to include...		(/etc/ansible/hosts)

![](https://github.com/JMPence89/Elk-Stack/blob/main/hosts_file.png)
     
- Run the playbook, and navigate to /etc/ansible to check that the installation worked as expected.

### To run playbooks:

![](https://github.com/JMPence89/Elk-Stack/blob/main/Deployment_commands.png)

### To access Kibana along with Filebeats and Metricbeats:

http://104.42.155.151:5601/app/kibana		(ELK VM must be running in order to access)

![](https://github.com/JMPence89/Elk-Stack/blob/main/Filebeat_Metricbeat_Screenshots/Filebeat.png)

![](https://github.com/JMPence89/Elk-Stack/blob/main/Filebeat_Metricbeat_Screenshots/Metricbeat.png)
