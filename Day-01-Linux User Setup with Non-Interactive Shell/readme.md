## Problem Statement

To accommodate the backup agent tool's specifications, the system admin team at xFusionCorp Industries requires the creation of a user with a non-interactive shell.  
Create a user named **yousuf** with a non-interactive shell on **App Server 3**.

**Note:** You can find the infrastructure details by clicking on the **Details of all Users and Servers** button.

---

## Before Directly Jumping to the Problem, Let’s Break It Down

### 🤔 What does "non-interactive shell" mean, and why do we create it?

- The user must **NOT** be able to log in  
- No SSH access  
- No terminal interaction  
- Service-only account  

---

## Types of Users in Linux

There are two types of users:

1. **Normal User (Human User)**
2. **System User (Service-Only Account)**

We create these “fake” users because Linux requires every process to have an owner.  
However, we block the shell because programs don’t need to type commands — only humans do.

The biggest reason for this is **security**.

If a hacker manages to break into your web server (like Apache or Nginx), they effectively "become" the user that is running that service.

- **If the service is running as a normal user:**  
  The hacker gets a shell, can run commands, and may find a way to access personal files.

- **If the service is running as a service account (with no shell):**  
  The hacker is restricted. Even if they break in, they cannot log in or run commands because there is no shell (such as `/bin/bash`) available.  
  The door is effectively locked from the inside.

---

## Real-World Example: Web Server

Imagine you have a website. The website needs to read your HTML files to display them.

- You create a user called `www-data`
- You give `www-data` permission to read only the `/var/www/html` directory
- You set its shell to `nologin`

Now, if a malicious user finds a vulnerability in your website:
- They can only see what `www-data` can access
- They cannot log into your server
- They cannot access private files
- They cannot change system settings

