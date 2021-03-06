![image](https://user-images.githubusercontent.com/38517925/86527948-5f983e80-bec1-11ea-9be7-03a6cc7792c8.png)

# INTRODUCTION
---------------

This playbook is intended to install and configure *KUBERNETES Cluster* on RHEL/CentOS 7,8 by **Kubeadm**.

**Note**: With RHEL OS you may face issues while installing docker lastest version if the OS is itself on old version.

Read this document carefully to have more understanding about this ansible playbook.

![image](https://user-images.githubusercontent.com/38517925/86524357-5abe9500-be97-11ea-8f15-d997b4ce7d3e.png)

## RESOURCE REQUIREMENTS
The playbook is intended to run on VM's with *atleast* **2 cores** and **900MB RAM** allocated. So please make sure, we have this much amount of resources available, else the playbook will fail. 

## VARIABLES DECLARATION
-----------------------

Variables need to declared inside deploy_kubernetes/defaults/main.yml

1. KUBERNETES_MASTER => The node fqdn or hostname who will act as Kubernetes Cluster master.

2. MASTER_IP_ADDRESS => IP address of the above kubernetes master 

3. Other variables declared in deploy_kubernetes/vars/main.yml

###### PRE-REQUISITES

- Basic knowledge of Linux, Git.
- Base OS repository should be configured.
- Internet connectivity of VM's (or all required respoitory configured offline)
- Communication already working between ansible control node and managed nodes.

###### INVENTORY SETUP

One can use it's own inventory or create it's own inventory.
Replace the hostnames in "inventory" file present here with hostnames of your environment. 

# USAGE
------------------------

Step | Description | Commands
------ | ----------- | --------
1 | Download this playbook in your ansible server | # git clone https://github.com/HemantGangwar/kubernetesCluster.git
2 | Enter into the directory created | # cd kubernetesCluster
3 | Update inventory file provided here with your node names. | # vi inventory
4 | Update deploy_kubernetes/defaults/main.yml with required parameter | (example) KUBERNETES_MASTER: master.lab.example.com
5 | Now execute the playbook | # ansible-playbook kubernetes.yml OR ansible-playbook kubernetes.yml -e KUBERNETES_MASTER=master.lab.example.com


Note:  *The playbook is fully idempotent and can be safely used multiple times.*

It contains 3 segments:

1. Pre-Requsisites taking care of Run time disabling of selinux and switching off swap.
2. A role named deploy_kubernetes containing master and worker deployment.
3. Post-Requisite taking care of setting up Networking(weave) for Cluster. 

Execution of playbook can be viewed at : https://www.youtube.com/watch?v=Lns4th54zPM&t=106s

AUTHOR
--------
This playbook is written by Hemant Gangwar, you can read more about author at https://learningtechnix.wordpress.com or follow on LinkedIN https://www.linkedin.com/in/hemant-gangwar-6a677b19/

BUG FIXES
-----------
1. In version 30 June 2020 fixed an issue with playbook requiring static master name while joining Kubernetes nodes
2. In version 10 July 2020 fixed issue of deprecated, package installation warning. And updated Inventory description.
3. In version 5 Aug 2020 fixed dependency issue used in case of RedHat OS.
