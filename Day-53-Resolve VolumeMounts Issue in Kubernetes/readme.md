
### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-
We encountered an issue with our `Nginx` and `PHP-FPM` setup on the Kubernetes cluster this morning, which halted its functionality. Investigate and rectify the issue:

The pod name is `nginx-phpfpm` and configmap name is `nginx-config`. Identify and fix the problem.
Once resolved, copy `/home/thor/index.php` file from the jump host to the `nginx-container` within the nginx document root. After this, you should be able to access the website using Website button on the top bar.

Note: The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.


# Solution :-

1. Modify Pod YAML file

  ``` bash
      kubectl get pod nginx-phpfpm -o yaml > nginx-phpfpm.yml
      vi nginx-phpfpm.yml
  ``` 

2. Edit the file

  from this 
  ``` text
    - name: php-fpm-container
      volumeMounts:
      - mountPath: /usr/share/nginx/html
        name: shared-files
  ```

  to this 
  ``` text
    - name: php-fpm-container
      volumeMounts:
      - mountPath: /var/www/html
        name: shared-files
  ```

 Now both the container use :- `/var/www/html` , for more detail read .yml file attached with the directory

3. Recreate Pod from the yml file of pod 

    ``` bash
        kubectl delete pod nginx-phpfpm
        kubectl apply -f nginx-phpfpm.yml
    ```

4. Copy file from the host to container

  syntax :- > kubectl cp <local_file_path> <pod_name>:<destination_path> [options]

  ``` bash
      kubectl cp /home/thor/index.php nginx-phpfpm:/var/www/html/index.php -c nginx-container
  ```

5. Access the website by click the given button 


