

### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-

The Nautilus DevOps team is delving into Kubernetes for app management. One team member needs to create a deployment following these details:
- Create a deployment named `nginx` to deploy the application `nginx` using the image `nginx:latest` (ensure to specify the tag)

Note: The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.


# Solution 

1. Create a file named `deployment-manifest.yml` and paste the content in the file 

    ```bash
      vi deployment-manifest.yml
    ```

    now paste the below content inside the file 

    ```text
      
      kind: Deployment
      apiVersion: apps/v1
      metadata:
        name: nginx
        labels:
          app: nginx
      spec:
        selector:
          matchLabels:
            app: nginx
        template:
          metadata:
            labels:
              app: nginx
          spec:
            containers:
              - name: nginx-container
                image: nginx:latest

    ```

2. Run the command to create and run a pod deployment

    ``` bash 
        kubectl apply -f deployment-manifest.yml
    ```

3. Verfiy the deployment using the below command 

    ``` bash
        kubectl get all
    ```

    - The above command will give all the resources running

    ``` text
        thor@jump-host ~$ kubectl get all
        NAME                         READY   STATUS    RESTARTS   AGE
        pod/nginx-6554fcb65f-2gll7   1/1     Running   0          21s

        NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
        service/kubernetes   ClusterIP   10.43.0.1    <none>        443/TCP   39m

        NAME                    READY   UP-TO-DATE   AVAILABLE   AGE
        deployment.apps/nginx   1/1     1            1           21s

        NAME                               DESIRED   CURRENT   READY   AGE
        replicaset.apps/nginx-6554fcb65f   1         1         1       21s
    ```


