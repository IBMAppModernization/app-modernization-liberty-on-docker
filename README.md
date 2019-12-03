# IBM Client Developer Advocacy App Modernization Series

## Lab - Build and run a  WebSphere Liberty app with Docker

## Overview

The lab illustrates how to build a simple WebSphere Liberty app with Docker


### Step 1: Logon into the Web terminal
1.1 Login into your terminal environment with the URL and credentials provided by your instructor


### Step 2: Create unique port number for your instance of Liberty

2.1 Run the following command to set an environment variable for a unique port based on your user identifier from the instructor (e.g. For example if your user id is **user020** your port number should be **30020**  ie 020 appended to 30)

    ```bash
    export LIBERTYPORT=30NNN
    ```

### Step 3: Create unique name  for your Liberty image

3.1 Run the following command to set an environment variable for a unique image name based on your user identifier from the instructor (e.g. For example if your user id is **user020** your image name  should be **liberty-user020**)

    ```bash
    export LIBERTYIMG=liberty-userNNN
        ```

### Step 4: Clone the sample  app repo

4.1  From the client terminal window clone the following Git repo with the app used in this lab

   ```bash
   git clone https://github.com/IBMAppModernization/liberty-hello-world-app.git
   cd liberty-hello-world-app
   ```

### Step 5: Build a Docker image for the app

5.1 From the client terminal window build the Docker image.

    ```bash
    docker build -t $LIBERTYIMG .
    ```

### Step 6: Run the  image for the app

6.1 From the client terminal window run the Docker image. (**Note:** Substitute your username for *userNNN* below. eg **liberty-user020**)

  ```bash
   docker run  --name $LIBERTYIMG -d  -p $LIBERTYPORT:9080  $LIBERTYIMG
  ```

### Step 7: Test the running  image

7.1 From the client terminal window test the Docker image. Verify that the curl command returns **Hello World**

  ```bash
   curl 127.0.0.1:$LIBERTYPORT/hello
  ```


## Cleanup

Run the following commands to cleanup (note: you can copy all the commands at once and post them into your command window)

   ```
   docker stop $LIBERTYIMG
   docker rm $LIBERTYIMG
   ```
