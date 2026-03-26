


### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-
The Nautilus DevOps team is working on to setup some pre-requisites for an application that will send the greetings to different users. There is a sample deployment, that needs to be tested. Below is a scenario which needs to be configured on Kubernetes cluster. Please find below more details about it.

1. Create a `pod` named `print-envars-greeting`.
2. Configure spec as, the container name should be `print-env-container` and use `bash` image.
3. Create three environment variables:
   - `GREETING` and its value should be `Welcome to`
   - `COMPANY` and its value should be `xFusionCorp`
   - `GROUP` and its value should be `Ltd`
4. Use command `["/bin/sh", "-c", 'echo "$(GREETING) $(COMPANY) $(GROUP)"']` (please use this exact command), also set its `restartPolicy` policy to `Never` to avoid crash loop back.
5. You can check the output using `kubectl logs -f print-envars-greeting command`.

Note: The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

# Things to know:- 

1. CrashLoopBackOff :- CrashLoopBackOff is a Kubernetes state indicating a container in a Pod is crashing repeatedly, and Kubernetes is waiting an increasing amount of time (backing off) between restarts. The pod starts, crashes, and restarts over and over, while Kubernetes waits exponentially longer (10s, 20s, up to 5 min) before trying again.

# Solution :-

1. Create a file that create a pod resource on k8s cluster

    ``` bash
      vi create-pod.yml
    ```
    
    paste the content below on it 

    ``` text
      
      kind: Pod 
      apiVersion: v1  
      metadata:
        name: print-envars-greeting
        labels:
          app: greeting
      spec:
        restartPolicy: Never 
        containers:
        - name: print-env-container
          image: bash:latest
          command: ["/bin/sh","-c",'echo "$(GREETING) $(COMPANY) $(GROUP)"']
          env:
          - name: GREETING 
            value: Welcome to
          - name: COMPANY 
            value: Stratos
          - name: GROUP 
            value: Ltd

    ```

2. Create/Apply a pod resources 

    ``` bash
        kubectl apply -f create-pod.yml
    ```

3. Verify the pod running 

    ``` bash
        kubectl get pods
    ```

4. Check the output 

    ``` bash
        kubectl logs -f print-envars-greeting 
    ```

