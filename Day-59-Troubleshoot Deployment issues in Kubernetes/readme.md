### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-

Last week, the Nautilus DevOps team deployed a redis app on Kubernetes cluster, which was working fine so far. This morning one of the team members was making some changes in this existing setup, but he made some mistakes and the app went down. We need to fix this as soon as possible. Please take a look.

The deployment name is `redis-deployment`. The pods are not in running state right now, so please look into the issue and fix the same.

Note: The kubectl utility on the jump-host has been configured to work with the Kubernetes cluster.


# Read before starting the solution

Note :- If you want to see the manifest yml file then you can run the command , this will return the output which you can redirect to new file 

    > `kubectl get deployment -o yaml > redis-deployment`


# Solution :-

1. Check what all the resources/object are up and running

   ```bash
       kubectl get all
   ```

   you will see :-

   ```text
       thor@jump-host ~$ kubectl get all
       NAME                                    READY   STATUS              RESTARTS   AGE
       pod/redis-deployment-6bc546f779-hz4ff   0/1     ContainerCreating   0          28s

       NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
       service/kubernetes   ClusterIP   10.43.0.1    <none>        443/TCP   36m

       NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
       deployment.apps/redis-deployment   0/1     1            0           28s
   ```

2. You can see the status of the pod `ContainerCreating` but wait for few min , it will get stuck on this status

   So run the command and describe the pod using the command below

   ```bash
       kubectl describe pods
   ```

   you will see :-

   ```text

       NAME                                          DESIRED   CURRENT   READY   AGE
       replicaset.apps/redis-deployment-6bc546f779   1         1         0       28s
       thor@jump-host ~$ kubectl describe pods
       Name:             redis-deployment-6bc546f779-hz4ff
       Namespace:        default
       Priority:         0
       Service Account:  default
       Node:             jump-host/10.244.247.204
       Start Time:       Sat, 28 Mar 2026 08:09:24 +0000
       Labels:           app=redis
                         pod-template-hash=6bc546f779
       Annotations:      <none>
       Status:           Pending
       IP:
       IPs:              <none>
       Controlled By:    ReplicaSet/redis-deployment-6bc546f779
       Containers:
         redis-container:
           Container ID:
           Image:          redis:alpin
           Image ID:
           Port:           6379/TCP
           Host Port:      0/TCP
           State:          Waiting
             Reason:       ContainerCreating
           Ready:          False
           Restart Count:  0
           Requests:
             cpu:        300m
           Environment:  <none>
           Mounts:
             /redis-master from config (rw)
             /redis-master-data from data (rw)
             /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-wtpps (ro)
       Conditions:
         Type                        Status
         PodReadyToStartContainers   False
         Initialized                 True
         Ready                       False
         ContainersReady             False
         PodScheduled                True
       Volumes:
         data:
           Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
           Medium:
           SizeLimit:  <unset>
         config:
           Type:      ConfigMap (a volume populated by a ConfigMap)
           Name:      redis-conig
           Optional:  false
         kube-api-access-wtpps:
           Type:                    Projected (a volume that contains injected data from multiple sources)
           TokenExpirationSeconds:  3607
           ConfigMapName:           kube-root-ca.crt
           Optional:                false
           DownwardAPI:             true
       QoS Class:                   Burstable
       Node-Selectors:              <none>
       Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                                   node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
       Events:
         Type     Reason       Age                From               Message
         ----     ------       ----               ----               -------
         Normal   Scheduled    48s                default-scheduler  Successfully assigned default/redis-deployment-6bc546f779-hz4ff to jump-host
         Warning  FailedMount  17s (x7 over 48s)  kubelet            MountVolume.SetUp failed for volume "config" : configmap "redis-conig" not found

   ```

   Here you can clearly see the 2 error :-
   1. > Warning FailedMount 17s (x7 over 48s) kubelet MountVolume.SetUp failed for volume "config" : configmap "redis-conig" not found

   2. > Image: redis:alpin

   Now try to fix these error

3. Run the command to see the correct name of the configmap

   ```bash
       kubectl get configmap
   ```

   ```text
       thor@jump-host ~$ kubectl get configmap
       NAME               DATA   AGE
       kube-root-ca.crt   1      37m
       redis-config       2      78s
   ```

4. Now finally edit the deployent file
   - attach the correct volumeMount , from name: redis-cofig to name: redis-config
   - fix the redis:alpin image to redis:alpine

   ```bash
       kubectl edit deployments.apps
   ```

   Now, vi editor is opened with the manifest file now edit the file and you are good to go

5. Verify the pods by running the command

   ```bash
      kubectl get pods
   ```

   you will see :-

   ```text
       thor@jump-host ~$ kubectl get pods
       NAME                                READY   STATUS    RESTARTS   AGE
       redis-deployment-5476b4ddd6-hs5ng   1/1     Running   0          8s
       thor@jump-host ~$ ^C
       thor@jump-host ~$
   ```


