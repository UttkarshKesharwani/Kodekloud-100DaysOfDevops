
### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-

Some of the Nautilus team developers are developing a static website and they want to deploy it on Kubernetes cluster. They want it to be highly available and scalable. Therefore, based on the requirements, the DevOps team has decided to create a deployment for it with multiple replicas. Below you can find more details about it:

- Create a `deployment` using `nginx` image with `latest` tag only and remember to mention the tag i.e `nginx:lates`t. Name it as `nginx-deployment`. The container should be named as `nginx-container`, also make sure `replica` counts are `3`.
- Create a `NodePort` type service named `nginx-service`. The `nodePort` should be `30011`.

Note: The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.


# Solution :- 

1. Create a deployment file and paste the content below into it .

    ``` bash 
        vi create-deployment
    ```

    ``` text
        
      apiVersion: apps/v1
      kind: Deployment
      metadata:
        name: nginx-deployment
        labels:
          app: nginx
          environment: production
      spec:
        replicas: 3
        selector:
          matchLabels:
            app: nginx  # It must match the pod labels
        template:
          metadata:
            name: nginx-container-template
            labels:
              app: nginx  # service will use this label  
          spec:
            containers:
            - name: nginx-container
              image: nginx:latest
              ports:
              - containerPort: 80

    ```

2. Create a service file and paste the content below into it .

    ``` bash 
        vi create-service
    ```

    ``` text
              
      apiVersion: v1
      kind: Service
      metadata:
        name: nginx-service
        labels:
          app: nginx
          environment: production
      spec:
        type: NodePort
        selector:
          app: nginx  # matches pod label (Service finds pods with this label)
        ports:
        - port: 80  # service port
          targetPort: 80  # container port
          nodePort: 30011   # external port (optional)

    ```

3. Make the kubernetes resource 

    ``` bash
        kubectl apply -f create-deployment
        kubectl apply -f create-service
    ```

4. Verify the resources 

    ``` bash
        kubectl get pods 
        kubectl get deployments
        kubectl get services
    ```

5. Verify if nginx-containers are running

    ```bash
        curl localhost:30011
    ```




### Things to know

1. Detailed Explanation

**targetPort**: This is the actual port where your application (e.g., Nginx, a Node.js app) is running inside the container. When traffic reaches the Kubernetes Service, it is forwarded to this specific port on the selected Pod. The targetPort and the application's listening port (often specified as containerPort in the Pod spec, though that is mostly informational) must match.

**port**: This is the port the Kubernetes Service itself listens on. Other services or pods within the cluster use the Service's ClusterIP and this port to communicate with the application. By default, if targetPort is not specified, it will use the same value as port.

**nodePort**: Used with a Service of type: NodePort to expose the application to the outside world. Kubernetes allocates a static port (by default, in the range 30000-32767) on all physical or virtual nodes. External users can access the service via <NodeIP>:<NodePort>, which then routes internally to the Service's port, and finally to the Pod's targetPort. 


2. The Flow of Traffic

A typical request journey through the different ports looks like this: 
  External Client: Accesses the service using the Node's IP and the nodePort (<NodeIP>:<NodePort>).
  Kubernetes Node: The node forwards the request from nodePort to the Service's internal port.
  Kubernetes Service: The Service's internal port load-balances and redirects the traffic to the appropriate Pod's targetPort.
  Pod/Container: The application is listening on the targetPort and processes the request. 
