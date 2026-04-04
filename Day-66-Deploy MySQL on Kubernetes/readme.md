

### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-

A new MySQL server needs to be deployed on Kubernetes cluster. The Nautilus DevOps team was working on to gather the requirements. Recently they were able to finalize the requirements and shared them with the team members to start working on it. Below you can find the details:

1. Create a PersistentVolume `mysql-pv`, its capacity should be `250Mi`, set other parameters as per your preference.
2. Create a PersistentVolumeClaim to request this PersistentVolume storage. Name it as `mysql-pv-claim` and request a `250Mi` of storage. Set other parameters as per your preference.
3. Create a deployment named `mysql-deployment`, use any mysql `image` as per your preference. Mount the PersistentVolume at mount path `/var/lib/mysql`.
4. Create a NodePort type service named `mysql` and set nodePort to `30007`.
5. Create a secret named `mysql-root-pass` having a key pair value, where key is `password` and its value is `YUIidhb667`, create another secret named `mysql-user-pass` having some key pair values, where first key is `username` and its value is `kodekloud_tim`, second key is `password` and value is `Rc5C9EyvbU`, create one more secret named `mysql-db-url`, key name is `database` and value is `kodekloud_db3`
6. Define some environment variables within the container:
  -  name: `MYSQL_ROOT_PASSWORD`, should pick value from secretKeyRef name: `mysql-root-pass` and key: `password`
  -  name: `MYSQL_DATABASE`, should pick value from secretKeyRef name: `mysql-db-url` and key: `database`
  -  name: `MYSQL_USER`, should pick value from secretKeyRef name: `mysql-user-pass` key key: `username`
  -  name: `MYSQL_PASSWORD`, should pick value from secretKeyRef name: `mysql-user-pass` and key: `password`

Note: The `kubectl` utility on the jump-host has been configured to work with the Kubernetes cluster.


# Solution :- 

1. Create a file and paste the content given below in the file 

  [pv file](./manifest/pv.yml)
  [pvc file](./manifest/pvc.yml)
  [secret file](./manifest/secret.yml)
  [secret1 file](./manifest/secret1.yml)
  [secret2 file](./manifest/secret2.yml)
  [deployment file](./manifest/deployment.yml)
  [service file](./manifest/service.yml)

2. Apply the resources 

  ```bash 
    
    kubectl apply -f pv.yml
    kubectl apply -f pvc.yml
    kubectl apply -f secret.yml
    kubectl apply -f secret1.yml
    kubectl apply -f secret2.yml
    kubectl apply -f deployment.yml
    kubectl apply -f service.yml

  ```

3. Verify the resources 

  ``` bash 
      kubectl get all -o wide
  ```