
### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-

The Nautilus DevOps teams is planning to set up a Grafana tool to collect and analyze analytics from some applications. They are planning to deploy it on Kubernetes cluster. Below you can find more details.

1.) Create a deployment named `grafana-deployment-devops` using any `grafana` image for Grafana app. Set other parameters as per your choice.

2.) Create `NodePort` type service with nodePort `32000` to expose the app.

`You do not need to make any configuration changes inside the Grafana app once deployed; just make sure you can access the Grafana login page`

Note: The kubectl utility on the jump-host has been configured to work with the Kubernetes cluster.



# Solution :-

1. Create a manifest file and paste the content given below in the file 

    ``` bash
        vi manifest.yml
    ```

    paste the file content given in the below file 

    [!here is the file](./manifest.yml)

2. Create the object 

    ``` bash
        kubectl apply -f manifest.yml
    ```

3. Verify the resource

    ``` bash
        kubectl get all
    ```

4. Click the `website` button

