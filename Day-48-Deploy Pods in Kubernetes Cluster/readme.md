

### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-

The Nautilus DevOps team is diving into Kubernetes for application management. One team member has a task to create a `pod` according to the details below:

1. Create a `pod` named `pod-nginx` using the `nginx` image with the `latest` tag. Ensure to specify the tag as `nginx:latest`.

2. Set the `app` label to `nginx_app`, and name the container as `nginx-container`.

Note: The kubectl utility on the jump-host has been configured to work with the Kubernetes cluster.



# Solution :- 

1. Create a file called `pod-manifest.yml` and then paste the following content

  `vi pod-manifest.yml`

  paste the text below 

  ``` text

    kind: Pod
    apiVersion: v1
    metadata:
      name: pod-nginx
      labels:
        app: nginx_app
    spec:
      containers:
      - name: nginx-container
        image: nginx:latest

  ```

2. Run the command to make the pod running

  ```bash 
    kubectl apply -f pod-manifest.yml
  ```

3. Verify the pod running 

  ``` bash
      kubectl get pods
  ```

