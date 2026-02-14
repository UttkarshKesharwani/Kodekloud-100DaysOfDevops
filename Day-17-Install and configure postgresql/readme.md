
### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-

The Nautilus application development team has shared that they are planning to deploy one newly developed application on Nautilus infra in Stratos DC. The application uses PostgreSQL database, so as a pre-requisite we need to set up PostgreSQL database server as per requirements shared below:
PostgreSQL database server is already installed on the Nautilus database server.
1. Create a database user `kodekloud_tim` and set its password to `BruCStnMT5`.
2. Create a database `kodekloud_db3` and grant full permissions to user `kodekloud_tim` on this database.
`Note`: Please do not try to restart PostgreSQL server service.


# Solution :- 

1. Login to the db server 

  ``` bash 
    ssh peter@stdb01
  ```

2. Switch to the postgres system user to check correctly running or not 
  `sudo -i -u postgres`
  `psql`
  You should see: `postgres=#`

3. Create Database User with given password

  ``` bash 
  CREATE USER kodekloud_tim WITH PASSWORD BruCStnMT5
  ```

4. Create Database

  ``` bash
    CREATE DATABASE kodekloud_db3;
  ``` 

5. Grant all privileges on the database to the user

  ``` bash 
    GRANT ALL PRIVILEGES ON DATABASE kodekloud_db3 TO kodekloud_tim;
  ```

5. Verify the user  by login
  > psql -U kodekloud_tim -d kodekloud_db3 -h localhost -W
  then enter pass `BruCStnMT5`.

  