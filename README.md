## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Click to see Image!](/James-Mutaka/cloud-project1/tree/main/Images/James-Diagram_CloudNetworkSecurity.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook.yml file may be used to install only certain pieces of it, such as Filebeat.
  -Enter the playbook file.Filebeat.yml
	                       Metricbeat.yml
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
-  What aspect of security do load balancers protect? What is the advantage of a jump box? 
   Load Balancers enhance availabilty of the Network through redundancy  
   Jump box prevents all Azure Virtual machines to be exposed to the public and also acts as point of filter for ports into the Azure Virtual machines.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- What does Filebeat watch for? Filebeats monitors for system files changes/Log Data, allowing real-time detection of important changes.
- What does Metricbeat record? records machine metrics such as uptime,memory or service running on target machine.

The configuration details of each machine may be found below.

| Name      	|         Function 	       | IP Address    | Operating System |
|---------------|------------------------------|---------------|------------------|
|Jump-box   	| Gateway,Ansible Provisioner  | 10.0.0.4      | Linux  (Ubuntu)  |
| Web1    	| DVWA Container, Web Server   | 10.0.0.5      | Linux  (Ubuntu)  |
| Web2    	| DVWA Container, Web Server   | 10.0.0.8      | Linux	 (Ubuntu) |
| Web3    	| DVWA Container, Web Server   | 10.0.0.9      | Linux  (Ubuntu)  |
| ELK Server    | ELK Container,Monitoring     | 10.1.0.4      | Linux  (Ubuntu)  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Whitelisted IP addresses 172.98.66.166 (JM-HomeOffice)
Machines within the network can only be accessed by Jump-box RedTeam 

-Which machine did you allow to access your ELK VM? JM-Homeoffice. What was its IP 
address? 172.98.66.166 access to ELK server  via Port 5601

A summary of the access policies in place can be found in the table below.

| Name    	     | Publicly Accessible | Allowed IP Addresses |
|--------------------|---------------------|----------------------|
| Jump Box 	     | Yes                 |172.98.66.166         |
| Web1  	     | No                  |52.191.0.184          |
| Web2     	     | No                  |52.191.0.184          |
| Web3  	     | No                  |52.191.0.184          |
| ELK Server         | Yes                 |172.98.66.166         |

### Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible? helps considerably with representation of Infrastructure as Code

 The playbook implements the following tasks:
- In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Install Docker and Ansible on Jump Box machine,enables playbook automation to push software services to other machines
- Add ELK VM to hosts file with seperate group header of ELK
- Run playbook file via ansible playbook command, thereby pushing tasks to all machines configured to receive

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
    ![Click to see details!](tree/main/Images/myansible.png)
    
    ![Click to see details!](/tree/main/Images/ansible_serviceUp.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- List the IP addresses of the machines you are monitoring_
 All the 3 Web Servers are being monitored - 10.0.0.5 | 10.0.0.8 | 10.0.0.9

We have installed the following Beats on these machines:
- Specify which Beats you successfully installed
  Filebeat and Metricbeat are installed all the 3 Web Servers VMs for monitoring purpose.

    ![Click to see details!](tree/main/Images/Filebeat-Kibana_SnapshotCapture.png)
    ![Click to see details!](tree/main/Images/Metricbeat-Kibana_snapshot.png)

These Beats allow us to collect the following information from each machine:
- In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
 Filebeat allows ELK Server to monitor files being accessed,keeping tracks of access(authorized or unauthorized users),
 if any changes are made to sensetives files such as the login (shadow or passwd files).Downloaded or transferred data.

   ![Click to see Image!](tree/main/Images/Filebeat.png)
   
   ![Click to see Image!](tree/main/Images/Kibana_Logs.png)

 Metricbeat allows the ELK Server to monitor metrics use; CPU, memory usage, and monitors what is coming in and out of the server at specified moments in time. 
 This allows regulation resources once volume of traffic is predetermined. 

  ![Click to see Image!](tree/main/Images/metric_kibana.png)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to container.
- Update the Playbook file to include...
- Run the playbook, and navigate to virtual machine(s) to check that the installation worked as expected.

 Answer the following questions to fill in the blanks:
  Which file is the playbook? Where do you copy it?
  -Playbook file is YAML read or saved as .yml and runs on Ansible. It's copied into container where Ansible playbook has been created on configured Docker.

- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- The Hosts file allows to modified and update on which machines to be deployed by making changes in respective device IP addresses.

 Which URL do you navigate to in order to check that the ELK server is running?
 Browser [ElK-Server Public IP:5601]
 
  As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
  
Sudo docker start [container name] i.e sudo docker start myansible
 sudo docker ps -a		    i.e  sudo docker ps -a
 sudo docker exec -ti [container name] bash  i.e sudo docker exec -ti myansible bash
 sudo ansible-playbook [.yml file to run] i.e sudo ansible-playbook penester1.yml
