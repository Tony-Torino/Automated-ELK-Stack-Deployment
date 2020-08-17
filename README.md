## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagram](images/Network-Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Full-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

- _Full-playbook.yml_

This document contains the following details:

- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly availability, in addition to restricting request to the network.

- _A load balancer defends against distributed denial of service (DDoS)_
- _The advantages of a Jump Box is that it allows you to acces and mannage all the devices in the network_

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the Logs and system metrics.

- _FileBeat collects log events and fowards them to the Elasticsearch for indexing._
- _Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch_

The
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.


| Name | Function | IP Address | Operating System |
| - | - | - | - |
| Jump Box | Gateway | 10.1.0.4 | Linux |
| Elk Server | Log server | 10.2.0.5 | Linux |
| Web-1 | web | 10.1.0.5 | Linux |
| Web-2 | backup | 10.1.0.6 | Linux |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

- _162.218.230.218_

Machines within the network can only be accessed by Jump Box.

- _The Elk vm can be access only by the jumbox ip adress 10.1.0.4_

A summary of the access policies in place can be found in the table below.


| Name | Publicly Accessible | Allowed IP Addresses |
| - | - | - |
| Jump Box | Yes | 162.218.230.218 |
| Web1/2 | no | 10.1.0.4 |
| Elk | no | 162.218.230.218 / 10.1.0.4 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

- _Ansible streamlines and simplifies cloud provisioning, configuration management, application deployment_

The playbook implements the following tasks:

- _Task 1: Install docker .io_
- _Task 2: Install Python3-pip_
- _Task 3: Install Python Docker Module_
- _Task 4: Increase the virtual memory for the container_
- _Task 5: Downlaod & Launch the Elk container_
  - set the ports that the container will run on

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![DockerPS](images/Docker_ps.PNG)

### Target Machines & Beats

This ELK server is configured to monitor the following machines:

- _Web-1 10.1.0.5_
- _Web-2 10.1.0.6_

We have installed the following Beats on these machines:

- _Filebeat & Metricbeat_

These Beats allow us to collect the following information from each machine:

- _Filebeat collects log events and Metricbeat collects metric and statistics for indexing._

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:

- Copy the filebeat-config file to ansible/Files.
- Update the config file to include Elk-server ptivate ip
- Run the playbook, and navigate to Kibana -> filebeat -> metric data  to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_

- _Which file is the playbook? Where do you copy it?_ _filebeat-configuration.yml_  **copy** : _/etc/filebeat/filebeat.yml_
- _Which file do you update to make Ansible run the playbook on a specific machine?
  - _hosts file_
- _How do I specify which machine to install the ELK server on versus which to install Filebeat on?_  _Elk-playbook_   add line `hosts: Elk`
- _Which URL do you navigate to in order to check that the ELK server is running? _http://[elk.ip]:5601/app/kibana_
