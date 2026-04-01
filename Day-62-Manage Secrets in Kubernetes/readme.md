### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/



# Problem Statement :-

The Nautilus DevOps team is working to deploy some tools in Kubernetes cluster. Some of the tools are licence based so that licence information needs to be stored securely within Kubernetes cluster. Therefore, the team wants to utilize Kubernetes secrets to store those secrets. Below you can find more details about the requirements:

- We already have a secret key file media.txt under the `/opt/` directory. Create a generic secret named `media`, it should contain the password/license-number present in `media.txt` file.
- Also create a pod `named secret-nautilus`.
- Configure pod's spec as container name should be `secret-container-nautilus`, image should be `ubuntu` with `latest` tag (remember to mention the tag with image). Use sleep command for container so that it remains in running state. Consume the created secret and mount it under `/opt/apps` within the container.
- To verify you can `exec` into the container `secret-container-nautilus`, to check the secret key under the mounted path `/opt/apps`. Before hitting the Check button please make sure pod/pods are in running state, also validation can take some time to complete so keep patience.

Note: The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.



# Solution :-

1. Create the Secret from file

    ``` bash
        kubectl create secret generic media --from-file=/opt/media.txt
    ```

2. Create a pod definition file (e.g., secret-pod.yaml) and paste the content below 

    ``` text
      apiVersion: v1
      kind: Pod
      metadata:
        name: secret-nautilus
      spec:
        containers:
          - name: secret-container-nautilus
            image: ubuntu:latest
            command: ["/bin/bash", "-c", "sleep 3600"]
            volumeMounts:
              - name: secret-volume
                mountPath: /opt/apps
                readOnly: true
        volumes:
          - name: secret-volume
            secret:
              secretName: media
    ```
  
3. Run the command 

  ``` bash
      kubectl apply -f secret-pod.yaml
  ```

4. Verify 

  ``` bash
      kubectl get pods
      kubectl exec -it secret-nautilus -- /bin/bash
      ls /opt/apps
      cat /opt/apps/media.txt
  ```


      
      