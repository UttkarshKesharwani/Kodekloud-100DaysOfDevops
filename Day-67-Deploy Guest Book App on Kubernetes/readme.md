

### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-


The Nautilus Application development team has finished development of one of the applications and it is ready for deployment. It is a guestbook application that will be used to manage entries for guests/visitors. As per discussion with the DevOps team, they have finalized the infrastructure that will be deployed on Kubernetes cluster. Below you can find more details about it.

`BACK-END TIER`

1. Create a deployment named `redis-master` for Redis master.
    - Replicas count should be `1`.
    - Container name should be `master-redis-devops` and it should use image `redis`.
    - Request resources as CPU should be `100m` and Memory should be `100Mi`.
    - Container port should be redis default port i.e `6379`.

2. Create a service named `redis-master` for Redis master. Port and targetPort should be Redis default port i.e `6379`.

3. Create another deployment named `redis-slave` for Redis slave.
    - Replicas count should be `2`.
    - Container name should be `slave-redis-devops` and it should use `gcr.io/google_samples/gb-redisslave:v3 image`.
    - Requests resources as CPU should be `100m` and Memory should be `100Mi`.
    - Define an environment variable named `GET_HOSTS_FROM` and its value should be `dns`.
    - Container port should be Redis default port i.e `6379`.

4. Create another service named `redis-slave`. It should use Redis default port i.e `6379`.

`FRONT END TIER`

5. Create a deployment named `frontend`.
    - Replicas count should be `3`.
    - Container name should be `php-redis-devops` and it should use `gcr.io/google-samples/gb-frontend@sha256:a908df8486ff66f2c4daa0d3d8a2fa09846a1fc8efd65649c0109695c7c5cbff` image.
    - Request resources as CPU should be `100m` and Memory should be `100Mi`.
    - Define an environment variable named as `GET_HOSTS_FROM` and its value should be `dns`.
    - Container port should be `80`.

6. Create a service named `frontend`. Its type should be NodePort, port should be `80` and its nodePort should be `30009`.

Finally, you can check the guestbook app by clicking on App button.
`You can use any labels as per your choice`.

Note: The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.


# Solution :-

1. Create the required resources and do checkout the below file 

    [frontend deployment file](./manifest/frontend-deployment.yml)
    [frontend service file](./manifest/frontend-service.yml)
    [backend deployment file](./manifest/redis-master-deployment.yml)
    [frontend service file](./manifest/redis-master-service.yml)
    [frontend service file](./manifest/redis-slave-deployment.yml)
    [frontend service file](./manifest/redis-slave-service.yml)

3. Navigate the correct directory and apply the resources 

    ```bash

      kubectl apply -f frontend-deployment.yml
      kubectl apply -f redis-master-deployment.yml
      kubectl apply -f redis-slave-deployment.yml
      kubectl apply -f redis-master-service.yml
      kubectl apply -f redis-slave-service.yml
      kubectl apply -f frontend-service.yml

    ```

4. Verify the resources

    ``` text
      
      thor@jump-host ~$ kubectl get all 
      NAME                                READY   STATUS    RESTARTS   AGE
      pod/frontend-69f877c54c-4nf7v       1/1     Running   0          80s
      pod/frontend-69f877c54c-6bzv4       1/1     Running   0          80s
      pod/frontend-69f877c54c-8mhqc       1/1     Running   0          80s
      pod/redis-master-74f7c4b664-5qlw8   1/1     Running   0          2m37s
      pod/redis-slave-f94878647-47vzw     1/1     Running   0          2m23s
      pod/redis-slave-f94878647-4bbwk     1/1     Running   0          2m23s

      NAME                   TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
      service/frontend       NodePort    10.43.95.255    <none>        80:30009/TCP   66s
      service/kubernetes     ClusterIP   10.43.0.1       <none>        443/TCP        78m
      service/redis-master   ClusterIP   10.43.210.78    <none>        6379/TCP       116s
      service/redis-slave    ClusterIP   10.43.133.158   <none>        6379/TCP       2m9s

      NAME                           READY   UP-TO-DATE   AVAILABLE   AGE
      deployment.apps/frontend       3/3     3            3           80s
      deployment.apps/redis-master   1/1     1            1           2m37s
      deployment.apps/redis-slave    2/2     2            2           2m23s

      NAME                                      DESIRED   CURRENT   READY   AGE
      replicaset.apps/frontend-69f877c54c       3         3         3       80s
      replicaset.apps/redis-master-74f7c4b664   1         1         1       2m37s
      replicaset.apps/redis-slave-f94878647     2         2         2       2m23s
      thor@jump-host ~$ 

    ```

4. Click the app button