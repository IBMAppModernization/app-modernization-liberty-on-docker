# IBM Client Developer Advocacy App Modernization Series

## Lab - Build and run a  WebSphere Liberty app with Docker

## Overview

The lab illustrates how to build a simple WebSphere Liberty app with Docker


### Step 1: Logon into the Web terminal
1.1 Login into your terminal environment with the URL and credentials provided by your instructor


### Step 2: Create unique port number for your instance of Liberty

2.1 Run the following command to set an environment variable for a unique port based on your user identifier from the instructor (e.g. For example if your user id is **user020** your port number should be **30020**  ie 020 appended to 30)

  ```
   export LIBERTYPORT=30NNN
  ```

### Step 3: Create unique name  for your Liberty image

3.1 Run the following command to set an environment variable for a unique image name based on your user identifier from the instructor (e.g. For example if your user id is **user020** your image name  should be **liberty-user020**)

  ```
   export LIBERTYIMG=liberty-userNNN
  ```

### Step 4: Clone the sample  app repo

4.1  From the client terminal window clone the following Git repo with the app used in this lab

  ```
   git clone https://github.com/IBMAppModernization/liberty-hello-world-app.git
   cd liberty-hello-world-app
  ```

### Step 5: Build a Docker image for the app

5.1 From the client terminal window build the Docker image.

  ```
   docker build --no-cache -t $LIBERTYIMG .
  ```

### Step 6: Run the  image for the app

6.1 From the client terminal window run the Docker image.

  ```
   docker run  --name $LIBERTYIMG -d  -p $LIBERTYPORT:9080  $LIBERTYIMG
  ```

### Step 7: Test the running  image

7.1 From the client terminal window test the Docker image. Verify that the curl command returns **Hello World**

  ```
   curl 127.0.0.1:$LIBERTYPORT/hello
  ```

### Step 8: Inspect the  running  image

8.1 From the client terminal window get a shell inside your running container.

  ```
   docker exec -it $LIBERTYIMG bash
  ```

8.2 Verify that your command prompt changes to ```bash-4.2$``` indicating that you are in a bash sheel in your running container

8.3 Look at the Liberty server logs

  ```
     cat /logs/messages.log
  ```
  Verify that  the log ends with something like the following (indicating that the application's single  servlet initialized correctly):

  ```
   [12/4/19 12:54:40:566 UTC] 00000038 com.ibm.ws.webcontainer.servlet   I SRVE0242I: [hw-web] [/] [HelloWorldServlet]: Initialization successful.
  ```

8.4 Look at your server.xml file

  ```
   cat /config/server.xml
  ```   
  Verify that the line is loading your app:
  ```
    <webApplication contextRoot="/" location="hw-web.war" />
  ```
8.5 Look at the folder that contains  all the installed applications

  ```
    ls -l /opt/ibm/wlp/usr/servers/defaultServer/apps
  ```   
  Verify that the your app is the only one installed:
  ```
    -rw-r--r-- 1 root root 4952 Dec  3 13:42 hw-web.war
  ```    

8.6 Look at the running processes in the container

  ```
   ps -ef
  ```   

  Verify that Liberty, your bash shell and the ps command are the only processes that appear:
  ```
    UID        PID  PPID  C STIME TTY          TIME CMD
    default      1     0  2 12:54 ?        00:00:28 /opt/ibm/java/jre/bin/java -java
    default    141     0  0 12:55 pts/0    00:00:00 bash
    default   1038   141  0 13:13 pts/0    00:00:00 ps -ef
  ```    
8.7 Exit the container shell

  ```
   exit
  ```

## Cleanup

Run the following commands to cleanup (note: you can copy all the commands at once and post them into your command window)

   ```
    docker stop $LIBERTYIMG
    docker rm $LIBERTYIMG
   ```
