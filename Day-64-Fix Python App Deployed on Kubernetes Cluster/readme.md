
### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-
One of the DevOps engineers was trying to deploy a python app on Kubernetes cluster. Unfortunately, due to some mis-configuration, the application is not coming up. Please take a look into it and fix the issues. Application should be accessible on the specified nodePort.

- The deployment name is `python-deployment-datacenter`, its using `poroko/flask-demo-app` image. The deployment and service of this app is already deployed.
nodePort should be `32345` and targetPort should be python flask app's default port.

Note: The kubectl `utility` on the jump-host has been configured to work with the Kubernetes cluster.

# Solution:- 

1. Verify the service which are running .

  ``` bash
      kubectl get all 
  ```

  ``` text
      thor@jump-host ~$ kubectl get all 
      NAME                                               READY   STATUS             RESTARTS   AGE
      pod/python-deployment-datacenter-65648dc9d-nhmzf   0/1     ImagePullBackOff   0          7m59s

      NAME                                TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)          AGE
      service/kubernetes                  ClusterIP   10.43.0.1     <none>        443/TCP          18m
      service/python-service-datacenter   NodePort    10.43.97.89   <none>        8080:32345/TCP   7m59s

      NAME                                           READY   UP-TO-DATE   AVAILABLE   AGE
      deployment.apps/python-deployment-datacenter   0/1     1            0           7m59s

      NAME                                                     DESIRED   CURRENT   READY   AGE
      replicaset.apps/python-deployment-datacenter-65648dc9d   1         1         0       7m59s
  ```

2. Describe the pods , since status is `ImagePullBackOff`.

    `kubectl describe pods`
    
    ``` text      
      thor@jump-host ~$ kubectl describe pods
      Name:             python-deployment-datacenter-65648dc9d-nhmzf
      Namespace:        default
      Priority:         0
      Service Account:  default
      Node:             jump-host/10.244.189.207
      Start Time:       Thu, 02 Apr 2026 14:59:46 +0000
      Labels:           app=python_app
                        pod-template-hash=65648dc9d
      Annotations:      <none>
      Status:           Pending
      IP:               10.22.0.9
      IPs:
        IP:           10.22.0.9
      Controlled By:  ReplicaSet/python-deployment-datacenter-65648dc9d
      Containers:
        python-container-datacenter:
          Container ID:   
          Image:          poroko/flask-app-demo
          Image ID:       
          Port:           5000/TCP
          Host Port:      0/TCP
          State:          Waiting
            Reason:       ImagePullBackOff
          Ready:          False
          Restart Count:  0
          Environment:    <none>
          Mounts:
            /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-s5pvx (ro)
      Conditions:
        Type                        Status
        PodReadyToStartContainers   True 
        Initialized                 True 
        Ready                       False 
        ContainersReady             False 
        PodScheduled                True 
      Volumes:
        kube-api-access-s5pvx:
          Type:                    Projected (a volume that contains injected data from multiple sources)
          TokenExpirationSeconds:  3607
          ConfigMapName:           kube-root-ca.crt
          Optional:                false
          DownwardAPI:             true
      QoS Class:                   BestEffort
      Node-Selectors:              <none>
      Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                                  node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
      Events:
        Type     Reason     Age                     From               Message
        ----     ------     ----                    ----               -------
        Normal   Scheduled  8m34s                   default-scheduler  Successfully assigned default/python-deployment-datacenter-65648dc9d-nhmzf to jump-host
        Warning  Failed     5m49s (x5 over 8m33s)   kubelet            Failed to pull image "poroko/flask-app-demo": failed to pull and unpack image "docker.io/poroko/flask-app-demo:latest": failed to resolve reference "docker.io/poroko/flask-app-demo:latest": pull access denied, repository does not exist or may require authorization: server message: insufficient_scope: authorization failed
        Warning  Failed     5m49s (x5 over 8m33s)   kubelet            Error: ErrImagePull
        Normal   BackOff    3m24s (x20 over 8m32s)  kubelet            Back-off pulling image "poroko/flask-app-demo"
        Warning  Failed     3m24s (x20 over 8m32s)  kubelet            Error: ImagePullBackOff
        Normal   Pulling    3m9s (x6 over 8m34s)    kubelet            Pulling image "poroko/flask-app-demo"
      thor@jump-host ~$ 
    ```

    - convert this by using command 

      `kubectl edit deployments.apps python-deployment-datacenter ` 

    ``` text
        spec:                                                                                                          
              containers:                                                                                                  
              - image: poroko/flask-app-demo                                                                               
                imagePullPolicy: Always                                                                                    
                name: python-container-datacenter  
                ports:                             
                - containerPort: 5000     
    ```
    to 

    ``` text
        spec:                                                                                                          
              containers:                                                                                                  
              - image: poroko/flask-demo-app                                                                               
                imagePullPolicy: Always                                                                                    
                name: python-container-datacenter  
                ports:                             
                - containerPort: 5000     
    ```
     
3. Now again check the pod , it will be running but when you click the website button it will not run so check the logs and u will be found that the python run on the port `5000`.

    `kubectl logs pod/python-deployment-datacenter-65648dc9d-nhmzf` 

    ``` text
        kubectl logs pod/python-deployment-datacenter-65648dc9d-nhmzf 
      * Serving Flask app "app.py"
      * Environment: production
        WARNING: Do not use the development server in a production environment.
        Use a production WSGI server instead.
      * Debug mode: off
      * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
    ```

    - Now check the service configration 

    `kubeclt get svc -o yaml > service.yml`

4. Now go to service file and change the port 

    `vi service.yml`

    change to this :- 
    ``` text
        ports:
      - nodePort: 32345
        port: 5000    
        protocol: TCP
        targetPort: 5000
    ```

5. Configure/Apply the file again

    `kubectl apply -f service.yml`

6. Click the app button 



