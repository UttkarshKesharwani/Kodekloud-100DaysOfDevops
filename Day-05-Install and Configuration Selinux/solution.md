

# Do follow for more such content
Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement
Following a security audit, the xFusionCorp Industries security team has opted to enhance application and server security with SELinux. To initiate testing, the following requirements have been established for App server 2 in the Stratos Datacenter:
- Install the required SELinux packages.
- Permanently disable SELinux for the time being; it will be re-enabled after necessary configuration changes.
- No need to reboot the server, as a scheduled maintenance reboot is already planned for tonight.
- Disregard the current status of SELinux via the command line; the final status after the reboot should be disabled.


# Why SELinux over normal Linux?

1. Linux normally protects files using: User, Groups, permissions.
  ❌ Problem with this system 
  - If: A program runs as rootOR a hacker breaks into a service running as root , "Nothing stops it from accessing everything"

2. SELinux adds an extra security lock.
  - Even if Linux permissions say: “Access allowed” .SELinux can still say: ❌ “No, you are not allowed”

# Real life analogy 
- Suppose you make a file in your normal user directory , now if the root user try to access your file, he can simply read, write ,execute your file. 
- So selinux , comes into the picture that lets you write the poilcies , based on that the user can get access for read/write. 


# Solution

1. Login into the server(given into your problem statement).

2. Install the remaining packages :-

  - By default, `selinux` is installed in your(few distros) system just you need to intalled remaining packages that lets you defines policy-rules and managmenet tools for selinux(it gives you some cli commands that lets you talk to the selinux) .

  => `cat /etc/selinux` , you will find `selinux` which is already installed configration in this directory by default(explore it).

  ```sh
    sudo dnf install -y selinux-policy selinux-policy-targeted policycoreutils policycoreutils-python-utils
  ```

3. Modify file in `/etc/selinux/config` , this file create after the remaining packages are installed :
  
  - `sudo vi /etc/selinux/config ` :- open file in vi editor
  - modify `SELINUX=disabled` 


## Good to Know?

### SELinux States

- **Enforcing**: Policies actively enforced, violations blocked
- **Permissive**: Policies logged but not enforced (audit mode)
- **Disabled**: SELinux completely turned off

### SELinux (Security-Enhanced Linux)

- **Purpose**: Mandatory Access Control (MAC) security framework
- **Modes**: Enforcing, Permissive, Disabled
- **Policies**: Targeted (default), Strict, MLS (Multi-Level Security)
- **Context**: Every file/process has security context (user:role:type:level)

### Configuration Files

- `/etc/selinux/config`: Main configuration
- `/var/log/audit/audit.log`: SELinux violations
- `/etc/selinux/targeted/`: Policy files

### Key Commands

- `getenforce`: Check current SELinux mode
- `setenforce 0/1`: Temporarily set permissive/enforcing
- `sestatus`: Detailed SELinux status
- `sealert`: Analyze SELinux denials
