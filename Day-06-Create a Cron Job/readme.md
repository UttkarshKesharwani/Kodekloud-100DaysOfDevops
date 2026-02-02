

# Do follow for more such content
Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-
The Nautilus system admins team has prepared scripts to automate several day-to-day tasks. They want them to be deployed on all app servers in Stratos DC on a set schedule. Before that they need to test similar functionality with a sample cron job. Therefore, perform the steps below:
- a. Install cronie package on all Nautilus app servers and start crond service.
- b. Add a cron */5 * * * * echo hello > /tmp/cron_text for root user.


# Things to know :- 
1. What is crontab? (Beginner-friendly)
> crontab is used to run commands or scripts automatically at a fixed time or interval.
- You don’t have to run the script manually.
- Linux runs it for you in the background.

- Simple definition :- `crontab` = time-based job scheduler in Linux


* * * * *  command_to_run(absolute path)
│ │ │ │ │
│ │ │ │ └─ Day of week (0–7) (Sun)
│ │ │ └── Month (1–12)
│ │ └─── Day of month (1–31)
│ └──── Hour (0–23)
└───── Minute (0–59)

> Cron jobs are user-specific. A cron added as root runs as root, even if it executes a user’s script.

# Solution 

1. Login to each server one by one , then switch into root using `sudo -i` (do it yourself)


2. Install `cronie` package into centos:

    ```sh
    sudo yum install cronie -y
    ```

3. Start crond service

    ```sh
    sudo systemctl enable crond
    sudo systemctl start crond
    ```

4. Create cron schedule:

    ```sh
    sudo crontab -e
    ```

    - crontab editor will be opene then write :- */5 * * * * echo hello > /tmp/cron_text

5. Verify crontab:

    ```sh
    sudo crontab -l
    ```

    and wait 5 minutes to check cron_text in /tmp/
