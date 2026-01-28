
# Do follow for more such content
Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

### Problem Statement :- 
Following security audits, the xFusionCorp Industries security team has rolled out new protocols, including the restriction of direct root SSH login.

> Your task is to disable direct SSH root login on all app servers within the Stratos Datacenter.

# Think to know

1. User-Specific Config (Most Common)
This is where you'll store your personal aliases, custom ports, and private key mappings.
> Path: ~/.ssh/config
Note: By default, this file often doesn't exist. You may need to create it manually:

2. System-Wide Config
This applies to every user on the machine. You usually need sudo to edit this.
>Path: /etc/ssh/ssh_config

3. SSH Server Config (Host Side)
If you are trying to configure how the machine receives connections (e.g., changing the listening port), that is a different file:
>Path: /etc/ssh/sshd_config 


# commands to know

You should now how `sed` command works

- `sed` :- It is non-interactive tool used for filtering and transforming text. It lets you filter or transform text from a file with or without modifing/overwrite the same file.

> sed [options] 'commands' file



