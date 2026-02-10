# Do follow for more such content
Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-
We have one of our websites up and running on our Nautilus infrastructure in Stratos DC. Our security team has raised a concern that right now Apache’s port i.e `8083` is open for all since there is no firewall installed on these hosts. So we have decided to add some security layer for these hosts and after discussions and recommendations we have come up with the following requirements:

1. Install iptables and all its dependencies on each app host.
2. Block incoming port `8083` on all apps for everyone except for LBR host.
3. Make sure the rules remain, even after system reboot.



# Things to know :-

1. What is firewall ?
- A firewall is a crucial network security system that monitors and controls incoming and outgoing traffic based on predetermined security rules, acting as a barrier between a trusted internal network and untrusted external networks like the internet.
Linux also provide you this firewall in the form of `iptables`

2. What is iptables ?
- Iptables is a command-line firewall utility for Linux that inspects, filters, and manages network packets.

Syntax :-
> iptables [ACTION] [CHAIN] [MATCH] [TARGET]

3. Core Concepts of iptables
- iptables has 3 main things:
  a. Tables
  b. Chains (Traffic flows through chains/direction) :- INPUT (Traffic coming INTO server) , OUTPUT (Traffic leaving server) , FORWARD (Traffic passing through server)
  c. Targets (Actions) :- ACCEPT(Allow) , DROP(Silently block) , REJECT(Block and notify)
   

- [Action] :- What do you want to do with the rule?. This tells iptables how to manage the rule itself, not the traffic.
  
  Action	Meaning
  `-A`	Append (add rule at end)
  `-I`	Insert rule at position
  `-D`	Delete rule
  `-L`	List rules
  `-F`	Flush (remove all rules)
  `-P`	Set default policy

- [CHAIN] :- Where is the traffic going? . Chain tells which direction of traffic the rule applies to.

  Chain	                  Meaning
  `INPUT`	          Traffic coming into server
  `OUTPUT`	        Traffic going out from server
  `FORWARD`	        Traffic passing through server

- [MATCH] :- Which traffic should match this rule? . This part defines the conditions. Firewall checks traffic and asks: Does this packet match these conditions?

   Option	             Meaning
  `-p tcp`	          Protocol
  `-s IP`             Source IP
  `-d IP`             Destination IP
  `--dport`	          Destination port
  `--sport`	          Source port
  `-i eth0`	          Input interface
  `-o eth0`	          Output interface

  Note :- In iptables, you can absolutely add multiple matches in a single rule (eg - block for all host except , LBR host)

- [TARGET] :- What action to take on matched traffic? . After matching, firewall decides what to do.

  Target	         Meaning
  `-j ACCEPT`	      Allow traffic
  `-j DROP`	        Block silently
  `-j REJECT`	      Block and send response
  `-j LOG`	          Log packet

  `-j` in iptables stands for "jump" and specifies the target action or chain to move to when a packet matches the rule.


Rememeber :- 
ACTION → What to do with rule
CHAIN  → Where traffic goes
MATCH  → Which traffic
TARGET → What action

4. Lets Understand through one example :-

> iptables -A INPUT -p tcp --dport 22 -j ACCEPT

Meaning:-
Packet comes in
If protocol is TCP and port is 22
jump to ACCEPT
Allow packet




# Solution :- 

Note :- iptables does NOT support OR/AND condition inside a single rule. You must create two rules:

 ```sh
    sudo yum install -y iptables iptables-services
    sudo iptables -A INPUT -p tcp --dport 6200 -s 172.16.238.14 -j ACCEPT
    sudo iptables -A INPUT -p tcp --dport 6200 -j REJECT
    sudo service iptables save
    ```

Kernal read the iptables from top to bottom so first we need to allow the LBR host and then reject all other host
