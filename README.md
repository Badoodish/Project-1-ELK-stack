# Project-1-ELK-stack
In this project, we created a virtual network with multiple VMs and containers running. We set up a dvwa container and an ELK container to monitor it.

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Project 1: Azure Virtual Network](https://github.com/Badoodish/Project-1-ELK-stack/blob/main/Images/Diagram.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select playbook files may be used to install only certain pieces of it, such as [Filebeat playbook](https://github.com/Badoodish/Project-1-ELK-stack/blob/main/Playbooks/filebeat-playbook.yml).


This document contains the following details:
- Description of thde Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application. Load balancing ensures that the application will be highly redundant, in addition to restricting access to the network. Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to both application and system logs. 

The configuration details of each machine are as follows:


| Name     | Function                 | IP Address | Operating System |
|----------|--------------------------|------------|------------------|
| Jump Box | Gateway                  | 10.0.0.4   | Linux            |
| Web-1    | Running DVWA application | 10.0.0.5   | Linux            |
| Web-2    | Running DWVA application | 10.0.0.6   | Linux            |
| ELK      | Running ELK application  | 10.1.0.4   | Linux            |



### Access Policies

The machines on the internal network are not exposed to the public Internet. Only the Jump Box machine can accept connections from the Internet. Access to Jump Box machine should be restricted to the public IP address of your own machine. Your public IP address can be found [here](https://ip4.me/). The remaining machines within the network should be configured so that they can only be accessed from the Jump Box by using the SSH protocol. 

A summary of the access policies in place are as follows:


| Name     | Publicly Accessible | Allowed IP Addrresses |
|----------|---------------------|-----------------------|
| Jump Box | Yes                 | User's public IP      |
| Web-1    | No                  | 10.0.0.4              |
| Web-2    | No                  | 10.0.0.4              |
| ELK      | No                  | 10.0.0.4              |



### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because for two key reasons. Automating configuration with Ansible reduces the risk of human-error during configuration and also enables an adminsitrator to easily perform horizontal scaling incase an application requires additional capacity.

The ELK installation playbook implements the following tasks:
1. Install docker on your ELK VM
2. Install Python on your ELK VM
3. Increase the virtual RAM of your ELK VM to 262144 
4. Download the ELK image container
5. Start docker service on your ELK VM


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker PS elk](https://github.com/Badoodish/Project-1-ELK-stack/blob/main/Images/docker_ps_output.PNG)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Name  | Private IP |
|-------|------------|
| Web-1 | 10.0.0.5   |
| Web-2 | 10.0.0.6   |


We have installed the Filebeats and Metricbeats on these machines. Filebeat is an add-on to the ELK stack which "monitors log files that you specify, and forward them to Elasticsearch." For example, you could configure your filebeat to monitor particular application logs. Metricbeat is a different add-on to the ELK stack which collects system and service information from the machine on which your ELK stack is running. For example, CPU usage or disk space.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the [elk playbook](./Playbooks/elk-playbook) file to the ~/etc/ansible/ directory. 
- Update the hosts file to include your elk machine. Click [here](https://github.com/Badoodish/Project-1-ELK-stack/blob/main/Images/etc_ansible_hosts.PNG) to see an example.
- Run the playbook, and navigate to http://<ELK.VM.External.IP>:5601/app/kibana to check that the installation worked as expected.


