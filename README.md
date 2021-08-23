# Automated ELK Stack Deployment
The files in this repository were used to configure the network dipicted below.

![AzureCloudDiagramA](https://user-images.githubusercontent.com/77220840/130520416-5d766be8-1697-48f3-a345-6b4588de553f.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above or lternatively, select portions of the file may be used to install only certain pieces of it such as Filebeat.

install-elk.yml![ELK  yml Playbook](https://user-images.githubusercontent.com/77220840/130521295-e7a5e5f2-d59e-4dd9-a5e2-ad3b053dd163.jpeg)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored 
- How to Use the Ansible Build

### Description of the Topology

The main puropse of this network is to explose a load-balanced and monitored insrance of DVWA, the D*amn Vulnerable Web Application.

Load balancing ensures that the application will be highly available and reliable, in addition to restricing traffic to the network.

- Load balancers protect the system from Denial-Of-Service attacks. Because it evenely distributes incoming web traffic and data, it helps prevent and mitigate the potential of a server overload.

- The advantage of a jumpbox is having the ability to access different web servers or networks while maintaing a controlled and secure connection. It acts as a configrued gateway between machines.

Integrating an ELK server allows users to eassily monitor the vulnerable VMs for changes to the file systems of the VMs and network as well as watch system metrics, such as CPU usage; attempted SSH logins; 'sudo' escalation failures; etc.

The configuration details of each machine may be found below

| Name        | Function | IP Address | Operating System |
|-------------|----------|------------|------------------|
| Jump Box    | Gateway  | 10.0.0.4   | Linux/ Microsoft |
| Web-1       | Webserver| 10.0.0.5   | Linux/ Microsoft |
| Web-2       | Webserver| 10.0.0.6   | Linux/ Microsoft |
| ELK Server  | Webserver| 10.1.0.4   | Linux/ Microsoft |

### Access Policies

The machines on the internal network are not exposed to the public internet.

Only the Jump Box machine can accept connections from the internet. Access to this machine is only allowed from the following IP address:
- 75.73.153.56 (My Host Machine)

Machines within the network can only be accessed by the Jump Box VM. The Jump Box VM was allowed access to the ELK Server VM with the private IP address of 10.0.0.4.

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
|  Jump Box  |        Yes          |      75.73.153.56    |
|   Web-1    |        No           |        10.0.0.4      |
|   Web-2    |        No           |        10.0.0.4      |
| ELK Server |        No           |        10.0.0.4      |

### Elk Configuration

Ansible was used to automate configuration of the ELK Server machine. No configuration was performed manually, which is advantageous because of the accessibility and ease of utilising Ansible. Ansible provides the installations and all of the required files. Being able to go to the site to copy the modules as formulate the playbook makes it a quick and cost-effective task. Doing it manually would be both time consuming and tedius, so the accessibility to Ansible is beneficial to all.

The playbook implements the following tasks:
  - First, it configures the ELK machine with Docker
  - Second, it installs the Python3 package, Pip.
  - Third, there is a Docker Python module that is installed.
  - Fourth, a Sysctl module was implemented for more memory.
  - Fifth, a Docker ELK container was downloaded.
  - Lastly, the Systemd Module enabled Docker on boot.

The following screenshot displays the configured ELK installation playbook:

![ElkPlaybook](https://user-images.githubusercontent.com/77220840/130529173-e9a47e06-d708-43e4-88b7-8b94fc0a87c7.jpeg)

The following screenshot displays the result of running 'docker ps' after successfully configuring the ELK instance:

![ELKRunningDockerPs](https://user-images.githubusercontent.com/77220840/130528893-a8c3854a-ae39-490b-8109-5c06c180db82.jpeg)

### Target Machines and Beats
This ELK server is configured to monitor the following machines:
  - Web-1 10.0.0.5
  - Web-2 10.0.0.6

We have installed the following Beats ont hese machines:
  - Filebeat
  - Packetbeat
  - Metricbeat

These beats allow us to collect the following information from each machine:
  - Filebeat: Collects data, such as log files, then monitors and sends it to the specified output.
  - Packetbeat: Collects packets on the network and traces all of the activity on that server.
  - Metricbeat: Collects metric data from the specified servers and monitors then sends it to the output. 
    - For example, metricbeat might monitor that a spike amount of users have been attempting to log into the system, and it will detect that data and record it.

### Using the Playbook
In order to use the playbook, one will need ot have an Ansible control mode already configured. Assuming they have such a control node provisioned:
  - SSH into the control mode
  - Update the file to include the .cfg file configurations and the playbook configuration
  - Run the playbook, and navigate to the Kibana website through the ELK server to check that the installation worked as expected.

### FAQ
1. Which file is the playbook? Where do you copy it?

The playbook file would be  the YAML file that one creates. Depending on what playbook one would want to run, can copy the configuration from sites such as Filebeat.

2. Which file does one update to make Ansible run the playbook on a specific machine?

One would update the .cfg file and ensure that the host section is accurate to their selected machines IP addresses.

3. How does one specify which machine to install the ELK server on versus which to install Filebeat on?

It can be specified through the ansible playbook.

4. Which URL does one have to navigate to in order to check that the ELK server us running?

They would navigate to http://*ElkServerMachineIP*:5601/app/kibana. For example, mine was http://13.64.91.233:5601/app/kibana. This should load the Kibana homepage.

The following screenshot displays an example of a successful Kibana connection:

![Browser Connection To Kibana](https://user-images.githubusercontent.com/77220840/130531010-123db7e7-ec1f-40a2-9af4-ab9a9236bbab.png)
