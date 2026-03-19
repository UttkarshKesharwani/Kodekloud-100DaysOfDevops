### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-

The Nautilus DevOps team has noticed performance issues in some Kubernetes-hosted applications due to resource constraints. To address this, they plan to set limits on resource utilization. Here are the details:

- Create a pod named `httpd-pod` with a container named `httpd-container`. Use the `httpd` image with the `latest` tag (specify as `httpd:latest`). Set the following resource limits:
- Requests: Memory: `15Mi`, CPU: `100m`
- Limits: Memory: `20Mi`, CPU: `100m`

Note: The `kubectl` utility on the jump-host has been configured to work with the Kubernetes cluster.


# Solution :- 

1. Create a file `create-pod.yml` and paste the content 

    ```bash
        vi create-pod.yml
    ```

    paste the content in the newly created file

    ``` text
            
      kind: Pod
      apiVersion: v1
      metadata:
        name: httpd-pod
        labels:
          app: httpd-pod 
      spec:
        containers:
          - name: httpd-container
            image: httpd:latest
            resources:
              limits:
                cpu: "100m"
                memory: "20Mi"
              requests:
                cpu: "100m"
                memory: "15Mi"

    ```

2. Create the pod using the below given command

  ``` bash
      kubectl apply -f create-pod.yml
  ```

3. Verfiy the pod 

    ``` bash
        kubectl get all
    ```

  you will see the content like 

  ``` text

    thor@jump-host ~$ kubectl get all 
    NAME            READY   STATUS    RESTARTS   AGE
    pod/httpd-pod   1/1     Running   0          8s

    NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
    service/kubernetes   ClusterIP   10.43.0.1    <none>        443/TCP   29m

  ```

4. For more details, describe the pod using 

    `kubectl get pod/httpd-pod`
