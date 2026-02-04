

# Problem Statement :- 
During the weekly meeting, the Nautilus DevOps team discussed about the automation and configuration management solutions that they want to implement. While considering several options, the team has decided to go with Ansible for now due to its simple setup and minimal pre-requisites. The team wanted to start testing using Ansible, so they have decided to use jump host as an Ansible controller to test different kind of tasks on rest of the servers.

> Install ansible version 4.9.0 on Jump host using pip3 only. Make sure Ansible binary is available globally on this system, i.e all users on this system are able to run Ansible commands.

# Thinks to know :-

1. What is ansible ?

  - Technical definition :- Ansible is an automation tool used to configure servers, deploy applications, and manage infrastructure automatically—so you don’t have to log in to each server and do repetitive work by hand.

  - Simple defintion :-  Imagine you have 10 or 100 servers and you want to:
    install nginx
    update packages
    start services
    copy config files
    Doing this manually = slow, error-prone, boring ❌
    Ansible does it in one command ✅


# Solution :-

  Since ansible is python tool, sudo apt installs software system-wide and removes control. So we use the python enviorment manager to download ansible 

  `sudo pip3 install ansible==4.9.0`

  