### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-
The Nautilus DevOps team needs to set up several docker environments for different applications. One of the team members has been assigned a ticket where he has been asked to create some docker networks to be used later. Complete the task based on the following ticket description:

1. Create a docker network named as `beta` on `App Server 2` in Stratos DC.
2. Configure it to use `macvlan` drivers.
3. Set it to use subnet `172.28.0.0/24` and iprange `172.28.0.0/24`.


# Things to know before proceeding to the solution :-

1. What are network in the docker ?
- Since docker container are always run on isolated environment , so if a particular container want to talk to the other running container they must be in a network to talk to each other . 

- There are 7 types of network given by the docker are :-

i) Bridge :- 
**Default Type**: This is the default network driver. If you do not specify a driver, this is what Docker uses.
**Use Case**: Ideal for running standalone containers that need to communicate on the same Docker host.
**Behavior**: Containers on a bridge network can communicate with each other, but they are isolated from the external network and require port mapping to be reachable from outside.

ii) Host :-
**Definition**: Removes network isolation between the container and the Docker host.
**Use Case**: Used for maximum performance when the container does not need its own isolated network stack, such as high-traffic web servers.
**Behavior**: The container uses the host's networking directly, meaning a containerized web server on port 80 will occupy port 80 on the host machine

iii) Overlay 
**Definition**: Connects multiple Docker daemons together.
**Use Case**: Essential for multi-host networking, particularly when using Docker Swarm or Kubernetes to run containers across different hosts.
**Behavior**: Allows containers on different physical hosts to communicate directly as if they were on the same network

iv) Macvlan 
**Definition**: Assigns a unique MAC address to a container.
**Use Case**: Useful for applications that need to behave like a physical device on the network, such as network monitoring tools or legacy applications.
**Behavior**: Containers connect directly to the host network interfaces without needing port mapping or Network Address Translation (NAT)

v) IPvlan
**Definition**: Similar to Macvlan, but it shares the host's MAC address instead of assigning a unique one.
**Use Case**: Preferred when there are restrictions on the number of MAC addresses allowed on a single network port.
**Behavior**: Offers finer control over both IPv4 and IPv6 addressing.

vi) None 
**Definition**: Completely disables networking for a container.
**Use Case**: Used when a container requires total isolation, such as a batch job processing sensitive local data.
**Behavior**: The container only has a loopback interface (lo) and cannot connect to external networks or other containers.

vii) Custom/User-Defined Bridge 
**Definition**: A bridge network created by the user (docker network create).
**Use Case**: Recommended for production over the default docker0 bridge.
**Behavior**: Offers automatic DNS resolution between containers on the same network.

2. Syntax to create a docker network 

  `docker network create [OPTIONS] <network_name>`


# Soultion :-

1. Login to the app server (do it by yourself)

2. Create a docker custom named network and give the driver, subnet , iprange .

  Syntax :-  `docker network create [OPTIONS] NETWORK_NAME`

  ``` bash
       docker network create --driver macvlan --ip-range=172.28.0.0/24 --subnet=172.28.0.0/24 beta
  ```

3. Verify the docker network 

  ``` bash 
      docker network ls 
  ```

  ``` text
      [steve@stapp02 ~]$ docker network ls
      NETWORK ID     NAME      DRIVER    SCOPE
      fa37ebc93ac9   beta      macvlan   local
      64dce12979ff   bridge    bridge    local
      848b1abafc0f   host      host      local
      2354252b1b40   none      null      local
  ```

4. To get the more detail of the network you created, then you can inspect the network

 ``` bash
    docker network inspect beta
 ```

 ``` text

    [steve@stapp02 ~]$ docker network inspect beta
    [
        {
            "Name": "beta",
            "Id": "a312018ff228f46fbf3d79243d0d1d4b962523f8996b3df6020eca70538687ef",
            "Created": "2026-03-11T09:23:24.695439704Z",
            "Scope": "local",
            "Driver": "macvlan",
            "EnableIPv6": false,
            "IPAM": {
                "Driver": "default",
                "Options": {},
                "Config": [
                    {
                        "Subnet": "172.28.0.0/24",
                        "IPRange": "172.28.0.0/24"
                    }
                ]
            },
            "Internal": false,
            "Attachable": false,
            "Ingress": false,
            "ConfigFrom": {
                "Network": ""
            },
            "ConfigOnly": false,
            "Containers": {},
            "Options": {},
            "Labels": {}
        }
    ]

 ```



