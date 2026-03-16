


### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-

A python app needed to be Dockerized, and then it needs to be deployed on App Server 2. We have already copied a requirements.txt file (having the app dependencies) under `/python_app/src/` directory on App Server 2. Further complete this task as per details mentioned below:


Create a Dockerfile under `/python_app` directory:

Use any `python` image as the base image.
Install the dependencies using `requirements.txt` file.
Expose the port `6000`.
Run the `server.py` script using CMD.

Build an image named `nautilus/python-app` using this Dockerfile.


Once image is built, create a container named `pythonapp_nautilus`:

Map port `6000` of the container to the host port `8094`.

Once deployed, you can test the app using curl command on App Server 2.

`curl http://localhost:8094/`


# Solution :-

1. Login to the app server and switched to the root user

2. Navigate the directory and make the Dockerfile 

  ``` bash
    cd /python_app
    vi Dockerfile
  ```

  ``` text
    FROM python:3.12-alpine

    WORKDIR /app

    COPY src/requirements.txt .

    RUN pip install -r requirements.txt

    COPY src/ .

    EXPOSE 5002

    CMD ["python","server.py"]
  ```

3. Build and run the container

  ``` bash 
    docker build -t nautilus/python-app .
    docker run -d --name pythonapp_nautilus -p 8091:5002 nautilus/python-app
  ```

4. Verify container 

  ```bash
    docker ps
  ```









