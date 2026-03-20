

### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-

An application currently running on the Kubernetes cluster employs the nginx web server. The Nautilus application development team has introduced some recent changes that need deployment. They've crafted an image `nginx:1.17` with the latest updates.

- Execute a rolling update for this application, integrating the `nginx:1.17` image. The deployment is named nginx-deployment.
- Ensure all pods are operational post-update.

`Note:` The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

# Solution:- 

1. Update the image using the command

    ``` bash
        kubectl set image deployment/nginx-deployment nginx-container=nginx:1.17
    ```

2. Then Verify Rollout

    ``` bash
        kubectl rollout status deployment/nginx-deployment
    ```

3. Verify pods 

    ``` bash
        kubectl get pods
    ```

    You should see:
      Old pods terminating
      New pods starting with nginx:1.17

4. Verfiy image whether image is updated

    ``` bash
        kubectl describe deployment nginx-deployment | grep Image
    ```