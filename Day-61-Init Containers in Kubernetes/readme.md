

### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-

There are some applications that need to be deployed on Kubernetes cluster and these apps have some pre-requisites where some configurations need to be changed before deploying the app container. Some of these changes cannot be made inside the images so the DevOps team has come up with a solution to use init containers to perform these tasks during deployment. Below is a sample scenario that the team is going to test first.

- Create a Deployment named as `ic-deploy-devops`.
- Configure `spec` as `replicas` should be `1`, labels `app` should be `ic-devops`, template's metadata lables `app` should be the same `ic-devops`.
- The `initContainers` should be named as `ic-msg-devops`, use image `fedora` with `latest` tag and use command `'/bin/bash'`, `'-c'` and `'echo Init Done - Welcome to xFusionCorp Industries > /ic/blog'`. The volume mount should be named as `ic-volume-devops` and mount path should be `/ic`.
- Main container should be named as `ic-main-devops`, use image `fedora` with `latest` tag and use command `'/bin/bash', '-c' and 'while true; do cat /ic/blog; sleep 5; done'`. The volume mount should be named as `ic-volume-devops` and mount path should be `/ic`.
- Volume to be named as `ic-volume-devops` and it should be an `emptyDir` type.

Note: The kubectl utility on the jump-host has been configured to work with the Kubernetes cluster.

# Solution :-

1. Create a deployment.yml file and paste the content present below:-

    ``` bash
        vi deployment.yml
    ```

    now , paste the below content 

    ``` text
      apiVersion: apps/v1
      kind: Deployment
      metadata:
        name: ic-deploy-devops

      spec:
        strategy:
        type: RollingUpdate
        rollingUpdate:
          maxUnavailable: 1
          maxSurge: 1

        replicas: 1
        selector:
          matchLabels:
            app: ic-devops

        template:
          metadata:
            labels:
              app: ic-devops
          spec:

            initContainers:
            - name: ic-msg-devops
              image: fedora:latest
              command: ['/bin/bash', '-c' , 'echo Init Done - Welcome to xFusionCorp Industries > /ic/blog']
              volumeMounts:
                - name: ic-volume-devops
                  mountPath: /ic

            containers:
            - name: ic-main-devops
              image: fedora:latest
              command: ['/bin/bash', '-c' , 'while true; do cat /ic/blog; sleep 5; done']
              volumeMounts:
                - name: ic-volume-devops
                  mountPath: /ic

            volumes:
              - name: ic-volume-devops
                emptyDir: {}
    ```

2. Apply the resources 

    ``` bash
        kubectl apply -f deployment.yml
    ```

3. Verify by running 

    ``` bash
        kubeclt get all -o wide
    ```

4. Whenever you create a `emptyDir` it store the data inside the node , do explore it by yourself 