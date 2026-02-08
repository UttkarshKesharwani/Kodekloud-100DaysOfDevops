# Tomcat Deployment Guide – Nautilus Project

##  Task Objective

Deploy a Java-based application on **App Server 3 (stapp03)** using Tomcat with the following requirements:

- Install Tomcat server.
- Configure Tomcat to run on port **5000**.
- Deploy the provided `ROOT.war` file.
- Ensure the application works on base URL:

```
http://stapp03:5000
```

---

## Prerequisites

- Access to Jump Host.
- SSH access to App Server 3 (`stapp03`).
- `ROOT.war` file available at:

```
/tmp/ROOT.war
```

on Jump Host.

---

##  Step 1: Login to App Server 3

From Jump Host:

```bash
ssh tony@stapp03
```

(Use the correct username provided in your environment.)

---

##  Step 2: Install Tomcat Server

For CentOS / RHEL:

```bash
sudo yum install tomcat -y
```

For Ubuntu:

```bash
sudo apt install tomcat9 -y
```

---

##  Step 3: Configure Tomcat to Run on Port 5000

Edit Tomcat configuration file:

```bash
sudo vi /etc/tomcat/server.xml
```

Find the connector configuration:

```xml
<Connector port="8080"
```

Change it to:

```xml
<Connector port="5000"
```

Save and exit the file.

---

##  Step 4: Copy ROOT.war from Jump Host

Run on Jump Host:

```bash
scp /tmp/ROOT.war tony@stapp03:/tmp/
```

Then login to `stapp03` and move the file:

```bash
sudo cp /tmp/ROOT.war /usr/share/tomcat/webapps/
```

---

##  Step 5: Start and Enable Tomcat

```bash
sudo systemctl start tomcat
sudo systemctl enable tomcat
```

---

##  Step 6: Verify Tomcat is Running on Port 5000

```bash
sudo ss -tulnp | grep 5000
```

---

##  Step 7: Test Application

Run:

```bash
curl http://stapp03:5000
```

If deployment is successful, the webpage content will be displayed.

---

##  How Deployment Works (Summary)

1. Tomcat starts and listens on port **5000**.
2. Tomcat scans the `webapps` directory.
3. `ROOT.war` is automatically extracted.
4. Application is deployed as root context (`/`).
5. Application becomes accessible directly from the base URL.

---

##  Expected Result

Application should be accessible at:

```
http://stapp03:5000
```

without any additional path.
