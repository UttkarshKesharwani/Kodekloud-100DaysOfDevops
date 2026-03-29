### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-

The Nautilus DevOps team is working on a Kubernetes template to deploy a web application on the cluster. There are some requirements to create/use persistent volumes to store the application code, and the template needs to be designed accordingly. Please find more details below:

Create a `PersistentVolume` named as `pv-xfusion`. Configure the spec as storage class should be `manual`, set capacity to `3Gi`, set access mode to `ReadWriteOnce`, volume type should be `hostPath` and set path to `/mnt/sysops` (this directory is already created, you might not be able to access it directly, so you need not to worry about it).

Create a `PersistentVolumeClaim` named as `pvc-xfusion`. Configure the spec as storage class should be `manual`, request `3Gi` of the storage, set access mode to `ReadWriteOnce`.

Create a `pod` named as `pod-xfusion`, mount the persistent volume you created with claim name `pvc-xfusion` at document root of the web server, the container within the pod should be named as `container-xfusion` using image `nginx` with `latest` tag only (remember to mention the tag i.e `nginx:latest`).

Create a node port type `service` named `web-xfusion` using node port `30008` to expose the web server running within the pod.

Note: The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

# Solution :-

1. Create a pod, pv , pvc and service from the given below file

   ![pod.yml file](./manifest%20files/pod.yml)
   ![pv.yml file](./manifest%20files/pv.yml)
   ![pvc.yml file](./manifest%20files/pvc.yml)
   ![service.yml file](./manifest%20files/service.yml)

2. Now apply files to make the resources

    ``` bash 

        kubectl apply -f pv.yml
        kubectl apply -f pvc.yml
        kubectl apply -f pod.yml
        kubectl apply -f service.yml

    ```

3. Verify if the resources is running correctly 

    ``` bash
        kubectl get all -o wide
    ```

    