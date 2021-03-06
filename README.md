# ELK-Project-1
Azure Network Setup
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Azure VN CW](https://user-images.githubusercontent.com/89741089/146595306-ea3021a0-1892-4819-9d31-9882d3a21437.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the config and yml files may be used to install only certain pieces of it, such as Filebeat.

- [Ansible.cfg](https://github.com/NomadCW/ELK-Project-1/blob/main/Files/Ansible/ansible.cfg)
- [Filebeat.yml](https://github.com/NomadCW/ELK-Project-1/blob/main/Files/Ansible/filebeat.yml)
- [Hosts file](https://github.com/NomadCW/ELK-Project-1/blob/main/Files/Ansible/hosts)
- [Metricbeat.yml](https://github.com/NomadCW/ELK-Project-1/blob/main/Files/Ansible/metricbeat.yml)
- [My Playbook.yml](https://github.com/NomadCW/ELK-Project-1/blob/main/Files/Ansible/my-playbook.yml)
- [Filebeat Playbook.yml](https://github.com/NomadCW/ELK-Project-1/blob/main/Files/ELK/filebeat-playbook.yml)
- [Metricbeat Playbook.yml](https://github.com/NomadCW/ELK-Project-1/blob/main/Files/ELK/metricbeat-playbook.yml)
- [Install Elk.yml](https://github.com/NomadCW/ELK-Project-1/blob/main/Files/ELK/install-elk.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Virtual Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

![Screen Shot 2021-12-15 at 3 47 29 PM](https://user-images.githubusercontent.com/89741089/146270178-f25e51bc-1bcc-4625-90ee-9cc8dc3c6451.png)

- The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

- Load balancing ensures that no single server has too much demand. This is done by spreading the workload across multiple servers. 

- What aspect of security do load balancers protect?
  Answer: Load balancing has an important role in regards to security as it helps defend against (DDoS) attacks, protects applications from emerging threats, authenticates user access, and helps simplify PCI compliance. 
- What is the advantage of a jump box?
  Answer: Added security. A jump box has been added as an access control to prevent the VM's exposure to the public as well as minimize open ports.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- What does Filebeat watch for?
  Answer: Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- What does Metricbeat record?
  Answer: Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.

| Name          | Function       | IP Address               | Operating System |
|---------------|----------------|--------------------------|------------------|
| Jump-Box      | Gateway        | 10.0.0.4 /52.255.170.193 | Linux            |
| Web-1         | Web Server     | 10.0.0.5                 | Linux            |
| Web-2         | Web Server     | 10.0.0.6                 | Linux            |
| ELK-SERVER    | ELK-SERVER     | 10.1.0.4                 | Linux            |
| Load Balancer | Load Balancer  | 20.119.53.18             | Linux            |
| Workstation   | Access Control | External (Public IP)     | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK Server can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Workstation Public IP through TCP 5601

Machines within the network can only be accessed by the Jump Box VM. Which machine did you allow to access your ELK VM? What was its IP address?
- Jump-Box-Provisioner IP : 10.0.0.4 (SSH port 22)
- Workstation Public IP to ELK (TCP port 5601)

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses              |
|---------------|---------------------|-----------------------------------|
| Jump-Box      |     No              | Workstation Public IP (SSH 22)    |
| Web-1         |     No              | 10.0.0.4 (SSH 22)                 |
| Web-2         |     No              | 10.0.0.4 (SSH 22)                 | 
| ELK-SERVER    |     No              | 10.1.0.4 (SSH 22)                 | 
| Load Balancer |     No              | Workstation Public IP (HTTP 80)   | 

### Elk Configuration

Ansible was used to automate configuration of the ELK machine (10.1.0.4). No configuration was performed manually, which is advantageous because Ansible allows a quick and efficient way to deploy apps. The ease of use is due to the ability to write a playbook allowing you to list required tasks without needing to write custom code. 

- The playbook implements the following tasks:
- Ansible playbook can specify a different group of machines as well as a different remote user:
![Playbook 1](https://user-images.githubusercontent.com/89741089/146653583-8c7096e3-0351-4765-9fca-edbed9537bac.png)
- To increase the system memory:

![Playbook 2](https://user-images.githubusercontent.com/89741089/146653593-a968f4b4-b9df-4f3a-911a-659ee2ac0562.png)
- Installation of services:

![Playbook 3](https://user-images.githubusercontent.com/89741089/146653855-1cde9c40-1017-4f84-8555-dfaab1a64194.png)
- Ports the container should start with:

![Playbook 4](https://user-images.githubusercontent.com/89741089/146653872-c55a4c58-e5a2-43e0-92d0-5af0202ed90b.png)

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img width="1212" alt="Screen Shot 2021-12-16 at 1 29 27 PM" src="https://user-images.githubusercontent.com/89741089/146436433-10774fee-2b2b-4f50-a388-2f5ab5b26ff1.png">

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 : 10.0.0.5
- Web-2 : 10.0.0.6

We have installed the following Beats on these machines:
 - Installed Beats: FileBeat and MetricBeat
 - ELK Server, Web-1, Web-2

These Beats allow us to collect the following information from each machine:
- FileBeat: data from the file system. (monitors specified files/log events and forwards for indexing)
- MetricBeat: collects machine metrics. (collects services and operating system metrics and ships them to a designated location)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

Update the hosts file to include ElK server

- Navigate to /etc/ansible/hosts and update file below:  
  [Hosts file](https://github.com/NomadCW/ELK-Project-1/blob/main/Files/Ansible/hosts)
- This is how the file should look:

 ![Hosts](https://user-images.githubusercontent.com/89741089/146658502-0692dc35-5c6b-47d7-b276-0b57ebe23e1a.png)


- Create a new playbook: touch /etc/ansible/install-elk.yml
- Next: nano install-elk.yml and copy and paste information from file below then save

- [Install Elk.yml](https://github.com/NomadCW/ELK-Project-1/blob/main/Files/ELK/install-elk.yml)
- (NOTE: be sure to SSH into you ELK machine to verify your connected before running the playbook.)
- Run the playbook using this command : ansible-playbook install-elk.yml

- To verify your ELK Server can load go to http://[your.VM.IP]:5601/app/kibana using the ELK Server IP to verify.
- If you see the picture below you have verified your ELK is up and running. 

![ELK Running](https://user-images.githubusercontent.com/89741089/146655049-749160ef-d0ef-47c4-afcf-4e433be709ad.png)

-Good Job! Your ELK installation is complete.

### More Information
- For more information on Ansible and and how it works with Azure visit: [Ansible](https://www.ansible.com/integrations/cloud/microsoft-azure)
- For more information on the ELK Stack visit: [ELK](https://www.elastic.co/elastic-stack/)
