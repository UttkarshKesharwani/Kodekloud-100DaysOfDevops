

# Do follow for more such content
Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement
The system admins team of xFusionCorp Industries has set up some scripts on jump host that run on regular intervals and perform operations on all app servers in Stratos Datacenter. To make these scripts work properly we need to make sure the thor user on jump host has password-less SSH access to all app servers through their respective sudo users (i.e tony for app server 1). Based on the requirements, perform the following:

> Set up a password-less authentication from user thor on jump host to all app servers through their respective sudo users.


# Thinks to know :- 

1. What is a Jump Host?

A Jump Host is like a security gate / middleman computer.
Instead of directly logging into important servers,you first log into one safe server → and from there jump into other servers. That’s why it’s called Jump Host (or Bastion Host).

Basically , you never expose the main server address to the internet, so we use the jump host
Your Laptop ─► Jump Host ─► Private Server

2. password-less authentication

There are two ways to login into the server using the keys ( private(stays on the local system) and public(stays on the server) ) and the password . Here we need to do password-less authentication , so we need to generate the keys(private/public) on the server and then send the public key to the other server .

# Command 

- `ssh-keygen` :- 
  - This creates:
  `~/.ssh/id_rsa `→ private key (DO NOT SHARE ❌)
  `~/.ssh/id_rsa.pub` → public key (safe to share ✅)

- `ssh-copy-id user@server_ip` :- Copy public key to the server . It will create .ssh directory for each app server if doesn't exist then copy paste host key to authorized_keys file.



# Solution

1. Generate SSH key:-

  `ssh-keygen -t rsa`

2. Copy SSH key to all App Server one by one 

  `ssh-copy-id user@server_ip` 

