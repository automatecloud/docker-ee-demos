# Proof of Concept
This file includes all the ingredients you need to do a successful Proof of Concept (PoC) with Docker Enterprise Standard & Advanced. 

## Content

We tried to bring all the content into a structure that makes sense and can help you to quickly find the right topics you are looking for. Here is the current table of content:

* Discovery Questions & Personal Roles (add Link)
* Scoping, Timing and Deliverals (add Link)
* Success Criterias & Out of Scope definitions (add Link)
* Checklists for Deployment Options and Planning Considerations (add Link)
* Implementation Steps & Run Books (add Link)

## Version

This version includes all the content you need to do a POC with the current Docker Enterprise Standard & Advanced release. This Guide is validated for UCP 2.2.x, DTR 2.4.x and Docker Enterprise Engine 17.06.x

## Contribution

Feel free to send us your ideas by creating issues or send us a pull request with updated content etc.

# Discovery Questions & Personal Roles

This section is for to prepare a Proof of Concept by using discovery questions and also find out the personal roles and responsiblities of everyone involved during the PoC.

## Example Questions

The following example questions can be used to prepare a Proof of Concept:

* Are you already using Docker?
* Are you familiar with the concept of managing applications with Docker?
* What is the skillset of your Developers when it comes to Docker?
* What is the skillset of your Operators when it comes to Docker?
* Do you have an application already running in Docker today? If not, have you picked an application to start with?
* What does your software architecture stack look like (i.e. application languages, databases, caching layer)?
* What are you doing for load balancing today? 
* How many servers are your applications running on today? 
* What operating system are you using for running your applications? 
* What are the use cases you need to prove?
* How do you define IF that use case is proven successful

## Personal Roles

For a successful PoC it is essential to have clear responsibilities 

Docker & Docker Partner - Helping to bring up a Docker EE environment:

* Solutions Engineer - [Name of Docker Solutions Engineer]
* Account Executive - [Name of Docker Account Executive]
* Alliances Manager - [Name of Docker Alliances Manager]

[Name of Partner] - Service Integrator/Reseller, provide support in coordination with Docker to stand up the environment

* Business Lead 
* Technical Lead 

Customer - Provide infrastructure and provision environments

* Business Lead
* Technical Lead
* Application Owner (if custom application will be used during the PoC) 


## Timing and and Scoping

A typical POC should be completed within 30 days, in preparation for the POC it is
advised to align the right technical resources and infrastructure and to dedicate to the completion of the POC. Technical resources and solutions engineers from Docker and the Partner mentioned above will be dedicated for those 30 days to help successfully deploy and deliver the POC.

### Example Timing for a PoC:

* 1 day Discuss and establish Success Criteria, sizing of timing and deliverables* 1 day Installation - Setup Docker EE Advanced (DTR and UCP) in HA mode across 6 nodes with valid certificates* 1 day Implementation - Setup Sample Voting Application - Push and Pull images, and deploy onto UCP* 1 day Implementation - [Service Discovery and Load Balancing Reference Architecture](
https://success.docker.com/Datacenter/Apply/Docker_Reference_Architecture%) 3A_Universal_Control_Plane_2.0_Service_Discovery_and_Load_Balancing* 1 day Review Success Criteria* 1 day Finalize POC and discuss next steps

### Example Scoping for a PoC:

The main question is what would a meaningful POC setup look like?

* What are the HA requirements?
* What is the Deployment infrastructure?
* What Operating systems will be used? Linux and/or Windows?
* Load Balancer Integrations?
* Sample applications?
* Container Networking?
* End to End Security

## Success Criterias & Out of Scope definitions

You can only proof the success of a concept if you define the success criterias at the beginning. 

What application will you use to prove out the success criteria? Some examples of success criteria include the following:

1. **Efficiency:** Reduce infrastructure costs with less footprint to run applications.

  **Deliverable:**
  
  * Demonstrate the ability to run more applications per node due to isolation provide by containers running in Docker EE engine. 

2. **Portability:** Run containers across multiple environments and easily migrate workloads between environments as needed

  **Deliverable:**

  * Demonstrate the ability to easily pull images from Docker Trusted Registry and deploy applications as a Stack using ’docker stack deploy’

3. **Agility with CI/CD workflow:** Continually build and deploy new versions of applications 
 
 **Deliverable:** 
 
 * Use a CI/CD engine (Jenkins) to trigger builds when new code is pushed. This will build images and deploy them gracefully onto nodes using Docker commands. This takes advantage of Swarm Mode services and rolling updates. 

4. **Resiliency:** If nodes fail, the application should still be operational. 
 
 **Deliverable:**
  
 * Use Swarm Mode services to demonstrate that when nodes fail containers are automatically rescheduled across the cluster. Use the Visualizer application to help visually represent status of containers. 

5. **End to End Security:** Ability to securely manage access to Docker containers, images, and repositories for securely building, running and deploying your applications.

  **Deliverable:** 
  
 * Enforce authorization and authentication by integrating UCP with authorization providers like LDAP/AD and enabling RBAC for UCP and DTR. 
 * Secure the development pipeline by scanning images and enforcing a policy for running Docker Images via Docker Content Trust. 
 * Deploy applications using secrets

## Checklists for Deployment Options and Planning Considerations

### Deployment Considerations

This document provides guidance on how to successfully stand up Docker EE and to use it to push and pull images from DTR and run them as containers in UCP.

To run Docker EE in HA mode, a minimum of 6 nodes are required to just support the Docker EE infrastructure, and do not take into account running any other containers or services. Additional nodes should be made available for resource nodes joined to the UCP cluster.

If CI/CD is a requirement, it is recommended to provision an additional node to run the CI/CD engine.

For a Docker EE POC built in an HA deployment scenario with CI/CD, ten (10) nodes would be recommended, where 4 of the 10 nodes are used explicitly for running applications and/or a CI/CD engine. 

For a Docker EE POC built in a non  HA deployment scenario with CI/CD, five (5) nodes would be recommended, where 3 of the 5 nodes would be used to explicitly run applications and/or a CI/CD engine.

### Deployment Options
The are two primary deployment options to consider for Docker EE:

1. **Manual OnPremise Installation:** If you are deploying Docker EE on premises or have a highly customized environment on a hosted cloud provider, this would be the the preferred option. Please read the **System requirements**:
 * [UCP systen requirements](https://docs.docker.com/datacenter/ucp/2.2/guides/admin/install/system-requirements/) 
 * [DTR system requirements](https://docs.docker.com/datacenter/dtr/2.4/guides/admin/install/system-requirements/)

 If you plan to do a **manual OnPremise offline** without any access to the Internet please make sure to do a pre download of all the necessary installation files:
 
  * UCP:
  * DTR:
  * Docker EE for CentOs:
  * etc.

2. **Cloud quickstart templates:** If you are looking for a quick way to deploy infrastructure and Docker EE in the cloud using a cloud template then you can use either of the templates we provide. Please read through the guides before deploying them.
 * [AWS Quickstart template](https://docs.docker.com/datacenter/install/aws/)
 * [Azure ARM template](https://portal.azure.com/#create/docker.dockerdatacenterdocker-datacenter)
 
 
### Checklist

Please use the following checklist to make sure you finished all the necessary preparation before we can start with the PoC:

| Checklist Item        | Details   
| ------------- |:-------------:| 
| 1. Personnel involved and roles |  | 
| 2. Schedule touchpoints (weekly, biweekly, etc?) |  | 
| 3. Determine scope of POC / Success criteria |     | 
|  * Timing (begin and end of POC) || 
|  * Selecting and containerizing an application in Docker |     | 
|  * Automated or manual build process? | |
|  * Source code repository| |
|  * CI tools/process| |
|4. DTR & UCP| |
| * HA||
| * Application Load Balancing||
| * Image storage backend||
| * Valid TLS certs||
| * Scanning||
| * Signing||
| * Integration with LDAP||
| * RBAC||
|5. Surrounding Ecosystem| |
| * Correct NTP configuration||
| * Correct DNS configuration||
| * Internet Access||
|||
|||
|||
|||
 
 Networking
 Volumes
 Config management
 Monitoring
 Logging

4. Provision Infrastructure of DDC
o Nodes
 Sizing
 Number of Nodes
 Location (AWS, Azure, on-
premises)
 Operating System
o Certificates (depends on scope of POC) o Load Balancers (depends on scope of
POC)

5. Install Docker EE Engine
o Devicemapper configuration (RHEL only)

6. Install UCP
a. Configure UCP
 Configure External Certs
 Configure LDAP
 Configure RBAC
 Configure Content Trust

7. Install DTR
a.
o o o
Configure DTR
Configure Shared Storage Create repository
Enable Security Scanning

8. Containerize selected application
o Build Docker Image for application
o Push Image to DTR
o Run application as container(s) on Swarm
Mode using Compose/Stacks

9. Deploy CI infrastructure
o Install CI/CD Engine (i.e Jenkins)
o Create jobs to build, push (and sign), and
deploy an image

10 Execute full pipeline using CI / Re-deploy application (application or security updates)

## Implementation Steps & Run Books

Before installing Docker EE, the following are a list of considerations to review when deploying Docker EE. Not all of these considerations are necessary when deploying Docker EE, however they are useful to review depending on the use cases outlined for the POC.

### Provision Infrastructure

HA (High Availability) Install
 Recommended 10 nodes: 
 3 nodes for UCP Manager
 3 nodes for Docker Trusted Registry
 4 worker nodes 

Non-HA Install
 Recommended 5 nodes:
 1 node for UCP Manager
 1 node for Docker Trusted Registry 
 3 worker nodes 

### Node Requirements

Supported OS: RHEL 7.x, Ubuntu 14.04/16.04, SLES 12.x
4GB of RAM (8GB RAM for DTR nodes where Image Scanning is Enabled)
30GB storage space
Unrestricted network connectivity between nodes (ports required described here)
Internet access to Docker Hub from all nodes (optional but preferred for ease of pulling the Docker images for UCP and DTR)
Sudo access credentials to each node

Minimum node infrastructure requirements (on-prem, vm, or cloud) - Note: if you are using the cloud quickstart templates, these decisions are already made for you, since the nodes are already provisioned:
a) 2 Core CPU (4 Core CPU recommended in production)
b) 4GB of RAM for UCP Controllers, 8GB RAM for DTR nodes where Image Scanning is
Enabled (16GB for each recommended in production)
c) 40GB storage space (SSD storage preferred for UCP controllers in production)
d) For RHEL/CentOS with devicemapper: separate block device OR additional free space
on the root volume group should be available for Docker storage
e) Unrestricted network connectivity between nodes
f) Unrestricted Internet access available from all nodes (optional but preferred)
Docker 2017 – Confidential
      
 g) Installed with Docker supported operating system ( http://success.docker.com/Get_Help/Compatibility_Matrix_and_Maintenance_Lifecycle )
h) Sudo access credentials to each node
i) Ports open for UCP:
https://docs.docker.com/datacenter/ucp/2.1/guides/admin/install/system-requirements/
j) Ports open for DTR:
https://docs.docker.com/datacenter/dtr/2.2/guides/admin/install/system-requirements/

Worker nodes - In addition to provisioning nodes for Docker infrastructure (UCP manager nodes and DTR replicas) you will need nodes to run your Docker containers. The sizing of and the number of worker nodes come with its own set of considerations.
a) Resources for worker nodes - The amount of resources will depend on the type, amount, and resource demands of applications that you will run inside of the nodes which run containers. Nodes that are VMS can be sized differently depending on the type of workloads that you expect to run on the node. A node can also be an entire physical blade or server from which you want to run the Docker engine. If a worker nodes resources are optimized/utilized only for a specific workload; then you can schedule the container on that node via a constraint. To help clarify this further, a couple of example scenarios are shown below and should be considered above the generally accepted worker node minimums of 2 vCPU and 4GB of memory:
i) You run a specific type of workload in a container (i.e. a java web application in a VM that utilizes 1 vCPU and 1GB of memory) and you are looking to run about 2 replicas of the container on a specific node. Thus you provision a worker node as VM that has 3 vCPU’s and 3GB of memory, and apply a node label ‘java-web-app’ to the node for that type of workload to be scheduled on. This node label must be provided by the compose file or docker service command you use to schedule this container.
ii) You plan to run a mixed group of applications as containers and want to size your nodes accordingly so containers get spread evenly across the nodes. Therefore, you must come up with a rough node sizing that can be utilized across all your nodes, based on either the standard VM size that your public or private infrastructure allows or a custom size that could be better utilized to run your applications in a mixed workload strategy.
iii) You have a fixed number of physical servers and want to run your containers on bare metal without VMs. The size of the node will be the size of the server that you install the engine on.

Number of worker nodes - The verified numbers that we know about are
what our largest customers are running which are in the low hundreds. Swarm itself is not a big bottleneck, as the connections from worker to manager are distributed across the manager nodes and then the writes are multiplexed back to the leader so Swarm communication is fairly efficient. There are verified Swarm 3K tests that ran 4000+ nodes in a single cluster on 3 manager nodes. The bigger bottlenecks will be the size of overlay networks and how many nodes a single overlay spans across.

Bring your own certs or Self-signed certs
a) Bring your own certs: A popular option for creating valid certificates in POC’s is LetsEncrypt to generate certificates based on a Trusted root CA. Two sets of certificates will need to be created, one for UCP and one for DTR.
b) Self-signed certs: Docker DataCenter creates self-signed certs for you by default for both UCP and DTR. Using this option will require you to trust the CA that is generated for DTR on each node in the UCP Swarm cluster for Docker Registry operations such as push and pull.

4) Docker image runtime storage: This is the storage system that is used for reading Docker image filesystem layers on the Docker engine.
a) Ubuntu: Ubuntu uses AUFS by default and we recommend using this as a stable option.
b) RHEL/CentOS: If you are using devicemapper we recommend that you re-configure
devicemapper to use direct-lvm mode instead of loop-lvm mode for performance reasons. Please follow steps on how to reconfigure your storage driver here: https://docs.docker.com/engine/userguide/storagedriver/device-mapper-driver/#/configur e-direct-lvm-mode-for-production

### Storage

Local image storage (i.e. graph driver)
 For RHEL recommended to use devicemapper in direct-lvm mode: link
Registry storage
 On premises: NFS
 Cloud: Azure Blob, S3, Swift
Volume storage
 Use NFS with local driver as reference implementation
 Use Docker Store storage plugins if needed 
 
 Shared storage for storing images at rest in Docker Trusted Registry: NFS (or other on-premises storage backend), Azure, S3 (or S3 compatible storage, i.e. Scality), Swift will need to be provisioned to use as the shared storage backend by DTR. S3 or Azure Blob storage integration is already taken care of for you by the cloud quickstart templates.
6) Persistent Storage for Containers: Managing persistent storage beyond the container lifecycle is a common question since containers are very ephemeral in nature. The best practice for storing persistent storage (i.e. database, filesystem, etc) is to use Docker volumes or Data Volume Containers.
a) Documentation on Docker Volumes:
https://docs.docker.com/engine/tutorials/dockervolumes/
b) An Introduction to Storage Solutions for Docker CaaS:
https://success.docker.com/Datacenter/Apply/An_Introduction_to_Storage_Solutions_for


### Networking

Swarm mode
 Networks using Overlay Driver
 Secrets for storing credentials and environment variables
 Reference Architecture: link

Classic Swarm 
 Reference Architecture: link

UCP 
 HTTP Routing Mesh: link 

### High Availability

High Availability
a) HA Deployment - Strongly recommended option, to replicate production workloads. In
order to install Docker EE in a highly available (HA) deployment, the following is required:
i) 6 nodes to install the base infrastructure - This will allow for the installation of three (3) Universal Control Plane (UCP) controllers and three (3) Docker Trusted Registry (DTR) replicas. NOTE: This is deployed by default via the Docker EE for AWS and Docker DataCenter for Azure cloud quickstart templates.
ii) A valid DNS entry should be created for the load balancer VIP for both UCP and DTR
iii) TCP load balancers should be available for both UCP and DTR
b) Non -HA deployment - the minimum number of nodes for the base infrastructure is two (2). This will allow for the installation of one (1) Universal Control Plane (UCP) controller and one (1) Docker Trusted Registry (DTR) replica Installing UCP and DTR on the same node is possible but not suggested.

### Continous Integration & Continous Deployment

A popular CI/CD engine is Jenkins and can be deployed both in a Docker Container or
standalone application in an Operating system. Jenkins supports the ability to run shell scripts as part of the Jenkins job and will allow you to run Docker native commands like docker build and docker push for building and pushing images.

Jenkins (reference implementation)
Build and push images
 Enable content trust 
 Build the image from Dockerfile 
 Tag the image with ‘docker tag <hostname>/<org>/<reponame>:<version>’
 Push the image to DTR with ‘docker push’ 

Pull and deploy images 
 Source client bundle 
 Deploy containers using `docker stack deploy’ from images on DTR


### Docker Content Trust

Docker Content Trust - Docker Trusted Registry integrates Notary out of the box and runs it in HA mode.
a) Overview of Content Trust:  https://docs.docker.com/engine/security/trust/content_trust/
b) Using Content Trust with DDC:
https://docs.docker.com/datacenter/ucp/2.1/guides/admin/configure/use-trusted-images-f or-ci/

### Swarm Mode and Classic Mode

Swarm Mode and Swarm Classic - Docker DataCenter runs both Classic Swarm and Swarm Mode. Containers are deployed on Classic Swarm via ‘docker run’ and ‘docker-compose’. In the new Swarm Mode containers are deployed using the new ‘docker service create’ command.
a) Review how to Swarm Mode works:
i) Nodes:  https://docs.docker.com/engine/swarm/how-swarm-mode-works/nodes/
ii) Services:
https://docs.docker.com/engine/swarm/how-swarm-mode-works/services/
Docker 2017 – Confidential
      
 iii) Security:
https://docs.docker.com/engine/swarm/how-swarm-mode-works/pki/
iv) Deploy containers via Services:
https://docs.docker.com/engine/swarm/swarm-tutorial/deploy-service/

### Example Applications

### Containerization of an App
Containerization of a Customer Application in Docker - Containerization of all applications would not be in scope of the POC. However, the containerization of at least one application will be useful for the purposes of successfully running a POC. There are three approaches to containerization that a lot of organizations take when deploying Docker. Each one of them takes advantage of the portability, efficiency, and security benefits that Docker provides.
a) Containerize Legacy Applications - Take legacy monolithic applications and deploy them as a container.
b) Transform Legacy to Microservices - Take legacy monolithic applications and start to containerize some of the services as individual containers. The eventual end goal would be to eventually have all services run as individual containers.
c) Accelerate New Applications - Start to build green field applications natively as services that are deployed in their own containers.

### License

Docker EE License - a Docker EE license (either trial or purchased) will be provided in your Docker Store account:  https://store.docker.com/?overlay=subscriptions . You can license your install after the install has completed through the Web UI of Universal Control Plane.

## Manual Installation

Manual installation steps
1) Read the following planning considerations:
https://docs.docker.com/datacenter/ucp/2.1/guides/admin/install/plan-installation/
2) Provision infrastructure with right OS (RHEL/CentOS, Ubuntu, SUSE)
3) If you are installing Docker EE offline, download Docker EE images for use offline for both UCP
and DTR:  https://docs.docker.com/datacenter/ucp/2.1/guides/admin/install/install-offline/
4) Install CS Engine on all nodes
a) If using RHEL and devicemapper, reconfigure your graph driver to be devicemapper on direct-lvm mode before installing Docker DataCenter: https://docs.docker.com/engine/userguide/storagedriver/device-mapper-driver/#/configur e-direct-lvm-mode-for-production . If this step is skipped, you will need to re-install Docker EE again after correctly configuring your graph driver.
5) Install UCP on one node and join additional master nodes
6) Join additional worker nodes to the Swarm cluster
7) Install DTR on one worker node and join additional replicas from worker nodes:
https://docs.docker.com/datacenter/dtr/2.2/guides/admin/install/
8) Install Docker EE and join additional worker nodes to run applications

Docker EE Advanced Implementation steps
A) Run a sample application
1) Docker pull and push to DTR:
https://docs.docker.com/docker-trusted-registry/repos-and-images/push-an-image/
a) Run ‘docker pull’ on an image hosted on Docker Hub
b) Tag the image with ‘docker tag <hostname>/<org>/<reponame>:<version>’
c) Push the image to DTR with ‘docker push’
 2) Create
a) Download Docker for Mac or Docker for Windows client
b) Download and source UCP Client Bundle
c) Create a service using ‘docker service create’:
https://docs.docker.com/datacenter/ucp/2.1/guides/user/services/deploy-a-service/
3) Docker Stack Deploy : The original method for deploying applications to Classic Swarm. This allows you to orchestrate containers together using a .yml file that describes environment variables, networks, and volumes that are used by the application that is composed of services.
a) Download and source UCP Client Bundle
b) Install Docker for Mac or Docker for Windows
c) Clone the example voting app ( https://github.com/docker/example-voting-app)  or a
simple application from Github
d) Run ‘docker stack deploy’’ in the directory that includes the compose file with the
commands described here:
https://docs.docker.com/datacenter/ucp/2.1/guides/user/services/deploy-app-cli/
4) Efficiency Success Criteria - Scale the application up and down using docker compose scale
5) Portability Success Criteria - Run the workload on another environment in AWS or Azure using docker pull and docker run commands


Continuous Integration and Deployment
1) Jenkins - Use Jenkins to run a CI/CD pipeline to build new images when code is committed. Also as a stretch, goal you can deploy containers from Jenkins in compose to automate the deployment process of the containers - Agility with CI/CD Success Criteria.
Docker 2017 – Confidential
services using Docker Swarm Mode
   
 a) Reference Architecture:
https://www.docker.com/sites/default/files/RA_CI%20with%20Docker_08.25.2015.pdf
b) Docker Jenkins Container instructions:  https://github.com/yongshin/leroy-jenkins

Service Discovery and Load Balancing
1) Deploy voting application using Docker Services in Swarm Mode and DDC:
https://success.docker.com/Datacenter/Apply/Docker_Reference_Architecture%3A_Universal_
Control_Plane_2.0_Service_Discovery_and_Load_Balancing
2) Deploy customer’s application using Docker Services in Swarm Mode and DDC:
3) Resiliency Success Criteria - Test resiliency by bringing down a node and rescheduling
containers on failed node to remaining nodes. Review the swarm rescheduling documentation:
https://docs.docker.com/swarm/scheduler/rescheduling/
4) Deploy services using HTTP Routing Mesh:
https://docs.docker.com/datacenter/ucp/2.1/guides/user/services/use-domain-names-to-access- services/


Additional Implementation Steps and Configuration
Below is a list of additional implementation steps that can help validate the POC according to the requirements of the customer. The considerations for this are discussed in the sections of “Planning Considerations for the POC”
● Deploy Config
● Node Management (Join Nodes, Pause/Drain, Promote HA Managers)
● Configure CA certs and HA load balancer (if necessary)
● Configure storage backend for DTR (S3, Azure Blob, etc)
● Deploy and Manage Applications
● Deploy an application (provide a reference app for testing) using services wizard,
volumes, networks
● Deploy the service with HTTP Routing Mesh
● Scale the application
● Perform Rolling Updates
● Use secrets with Services:
https://docs.docker.com/datacenter/ucp/2.1/guides/user/secrets
● Manage Users and Access Control (RBAC)
● Set up users and teams
Integrate LDAP/AD:
https://docs.docker.com/datacenter/ucp/2.1/guides/admin/configure/external-auth/
● Test out RBAC for services, networks, and volumes

Notary Enforcement
● Setup Notary local client with UCP user bundle
● Configure Content Trust signing enforcement:
https://docs.docker.com/datacenter/ucp/2.1/guides/admin/configure/only-allow-running-si
gned-images/
● Using Notary with CI/CD:
https://docs.docker.com/datacenter/ucp/2.1/reference/cli/fingerprint/
● Enable Image scanning for DTR images
● https://docs.docker.com/datacenter/dtr/2.2/guides/user/manage-images/scan-images-for
-vulnerabilities/
● Deploy additional applications
● Deploy applications in Swarm Mode with “docker service create” or Docker Compose
● Deploy applications in Compose using Secrets and HTTP Routing Mesh


## Docker EE Reference material & Additional Tips

Docker EE Best Practices and Design Considerations:
https://success.docker.com/Architecture/Docker_Reference_Architecture%3A_Docker_EE_Best
_Practices_and_Design_Considerations
● Reference Architectures:  https://success.docker.com/Architecture
● Maintenance Lifecycle:  https://success.docker.com/Policies/Maintenance_Lifecycle
● Compatability Matrix:  https://success.docker.com/Policies/Compatibility_Matrix

Take backups for both UCP and DTR once a day
Path of least resistance is to deploy Docker EE on AWS or Azure where we have official templates built out

 
