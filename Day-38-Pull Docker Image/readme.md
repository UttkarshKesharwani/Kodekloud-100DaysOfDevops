
### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-

Nautilus project developers are planning to start testing on a new project. As per their meeting with the DevOps team, they want to test containerized environment application features. As per details shared with DevOps team, we need to accomplish the following task:
1. Pull `busybox:musl`image on `App Server 3` in Stratos DC and re-tag (create new tag) this image as `busybox:local`.


# Things to know :- 

You can tag a Docker image either during the build process using the `docker build -t` command or by re-tagging an existing image using the `docker tag` command.

1. Tag an image during the build process 
This is the most common method, allowing you to name and version the image as it's created from a Dockerfile. 

  ``` bash
    docker build -t [YOUR_DOCKER_USERNAME]/[IMAGE_NAME]:[TAG_NAME] .
  ```

- [YOUR_DOCKER_USERNAME]:- Your Docker Hub username or organization name (e.g., mobywhale). This is necessary if you plan to push the image to a public registry.
- [IMAGE_NAME]:- A memorable name for your image (e.g., my-application).
- [TAG_NAME]:- A specific version identifier (e.g., 1.0.0 or stable). If omitted, Docker defaults to the latest tag.
- . :- Specifies the build context, which is the current directory containing the Dockerfile

> eg:- docker build -t yourusername/myapp:1.0.0 .



2. Tag an existing image

If an image has already been built (perhaps it only has an IMAGE ID or a default latest tag), you can add a new tag using the `docker tag` command.
 
  ```bash
    docker image tag [SOURCE_IMAGE][:TAG] [TARGET_IMAGE][:TAG]
    # or the shorter alias
    docker tag [SOURCE_IMAGE][:TAG] [TARGET_IMAGE][:TAG]
  ``` 
- [SOURCE_IMAGE][:TAG]: The name and optional tag of the existing image you want to reference. You can also use the IMAGE ID here.
- [TARGET_IMAGE][:TAG]: The new repository name and tag you want to apply. 

> eg:- docker tag yourusername/myapp:1.0.0 yourusername/myapp:stable


# Solution :-

1. Login to the app server (do it by yourself) 

2. Apply re-tag to image
  
  ``` bash 
      docker tag busybox:musl busybox:local
  ```

3. verify the image 

  ``` bash
      docker images
  ```



