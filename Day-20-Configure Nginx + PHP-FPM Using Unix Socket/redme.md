
### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-

The Nautilus application development team is planning to launch a new PHP-based application, which they want to deploy on Nautilus infra in Stratos DC. The development team had a meeting with the production support team and they have shared some requirements regarding the infrastructure. Below are the requirements they shared:

1. Install `nginx` on `app server 3` , configure it to use port `8093` and its document root should be `/var/www/html`.

2. Install php-fpm version `8.3` on app server 3, it must use the unix socket `/var/run/php-fpm/default.sock` (create the parent directories if don't exist).

3. Configure `php-fpm` and `nginx` to work together.

4. Once configured correctly, you can test the website using `curl http://stapp03:8093/index.php` command from jump host.

NOTE: We have copied two files, `index.php` and `info.php`, under `/var/www/html` as part of the PHP-based application setup. Please do not modify these files.



# Solution 

1. Login into App Server and run the following commands:

    ```sh
      sudo dnf install nginx -y
      sudo dnf module reset php -y
      sudo dnf module enable php:8.3 -y
      sudo dnf install php php-fpm -y
    ```

    - It will update packge repo
    - Install nginx and php with expected version

2. Configure php-fpm config:

    ```sh
    sudo mkdir -p /var/run/php-fpm
    sudo vi /etc/php-fpm.d/www.conf
    ```

    - `listen = /run/php-fpm/www.sock` change this line to `listen = /var/run/php-fpm/default.sock`

3. Configure nginx

    ```sh
    sudo vi /etc/nginx/nginx.conf
    ```

    - change port 80 to `8093`
    - change the DocumentRoot :- change `root` to `root /var/www/html`

4. Configure php with nginx

    ```sh
    sudo vi /etc/nginx/default.d/php.conf
    ```

    - change `fastcgi_pass php-fpm;` to this: `fastcgi_pass unix:/var/run/php-fpm/default.sock;`

5. Restart php-fpm and nginx

    ```sh
    sudo systemctl enable --now nginx
    sudo systemctl enable --now php-fpm
    ```

6. Test: `curl http://stapp01:8093/index.php`