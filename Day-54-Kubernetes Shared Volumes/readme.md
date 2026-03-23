

### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-

We are working on an application that will be deployed on multiple containers within a pod on Kubernetes cluster. There is a requirement to share a volume among the containers to save some temporary data. The Nautilus DevOps team is developing a similar template to replicate the scenario. Below you can find more details about it.

- Create a pod named `volume-share-nautilus`.
- For the first container, use image `fedora` with `latest` tag only and remember to mention the tag i.e `fedora:latest`, container should be named as `volume-container-nautilus-1`, and run a sleep command for it so that it remains in running state. Volume `volume-share` should be mounted at path `/tmp/ecommerce`.
- For the second container, use image `fedora` with the `latest` tag only and remember to mention the tag i.e `fedora:latest`, container should be named as `volume-container-nautilus-2`, and again run a sleep command for it so that it remains in running state. Volume `volume-share` should be mounted at path `/tmp/apps`.
- Volume name should be `volume-share` of type `emptyDir`.
- After creating the pod, `exec` into the first container i.e `volume-container-nautilus-1`, and just for testing create a file `ecommerce.txt` with the content `Welcome to xFusionCorp Industries` under the mounted path of first container i.e `/tmp/ecommerce`.
- The file `ecommerce.txt` should be present under the mounted path `/tmp/apps` on the second container `volume-container-nautilus-2` as well, since they are using a shared volume.

Note: The kubectl `utility` on the `jump-host` has been configured to work with the Kubernetes cluster.

# Solution:- 

1. Create a manifest file that create a pod and write the configration into it

    ``` bash 
        vi create-pod.yml
    ```

    and then paste the content into it 

    ``` text
      apiVersion: v1
      kind: Pod
      metadata: 
        name: volume-share-nautilus
      spec:

        volumes:
        - name: volume-share
          emptyDir: {}

        containers:
        - name: volume-container-nautilus-1
          image: fedora:latest
          command: ["/bin/bash", "-c", "sleep 3600"]
          volumeMounts:
          - name: volume-share
            mountPath: /tmp/ecommerce
        - name: volume-container-nautilus-2
          image: fedora:latest
          command: ["/bin/bash", "-c", "sleep 3600"]
          volumeMounts:
          - name: volume-share
            mountPath: /tmp/apps

    ```

2. Create the resource , i.e , pod from the manifest file 

    ``` bash
        kubectl apply -f create-pod.yml
    ```

3. Exec into First Container and then create a file given in the task 

    ``` bash
      kubectl exec -it volume-share-nautilus -c volume-container-nautilus-1 -- /bin/bash  
      echo "Welcome to xFusionCorp Industries" > /tmp/ecommerce/ecommerce.txt  
    ```

    Now verify the file and then exit from that container 

    ``` bash
      cat /tmp/ecommerce/ecommerce.txt
      exit
    ```

4. Verify in Second Container

    ``` bash
      kubectl exec -it volume-share-nautilus -c volume-container-nautilus-2 -- /bin/bash
      cat /tmp/apps/ecommerce.txt
    ```

    Expected Output

    `Welcome to xFusionCorp Industries`


# Things to know:- 

# Types of Kubernetes Volumes

1. **emptyDir**
=> Features:
  - Created when Pod starts
  - Deleted when Pod is removed
  - Stored on node
=> Use Case:
  - Temporary data
  - Sharing data between containers

2️. **hostPath**
=> Features:
  - Uses node’s filesystem directly
=> Problems:
  - Not portable
  - Security risk

3️. **Persistent Volume (PV)**
- Actual storage resource (disk, cloud storage)

4️.  **Persistent Volume Claim (PVC)**
- Request for storage by Pod
