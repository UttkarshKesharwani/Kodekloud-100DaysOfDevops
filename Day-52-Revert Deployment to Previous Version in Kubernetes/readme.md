### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-

Earlier today, the Nautilus DevOps team deployed a new release for an application. However, a customer has reported a bug related to this recent release. Consequently, the team aims to revert to the previous version.

There exists a deployment named `nginx-deployment`; initiate a rollback to the previous revision.
Note: The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

# Solution :-

1. Check each resources , what all resouces are running using the command :-

  ``` bash
      kubectl get all
  ```

2. Perform rollback to the previous version using command

  ``` bash 
      kubectl rollout undo deployment/nginx-deployment
  ```

3. Verfiy the rollout status

  ``` bash
      kubectl rollout status deployment/nginx-deployment  
  ```