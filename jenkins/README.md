#### # stand for big highighter, multiple # going to shorten the height of text
#### double tab is something where you can write your command

# Jenkins Basic ###

This is how you can run Jenkins as docker container. 

    docker run --name jenkins-docker -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home -d jenkins/jenkins:lts-jdk11
  
Above command execution is going to give us Jenkin master or controller. This would be enough to write and execute our pipeline jobs. However, for a team if they wanted to execute something concurrently we may need to have jenkins nodes acting as agent or slave, where actual execution going to happen. 

#### With enhanced supportability from Jenkins, now we are able to spin up ephemeral docker slave or agent which can be live / or start based on on-demand basis. 

# Pre-requisite for docker agent / slave
***
* docker plugin
* If you are going to use separate docker enabled host, to have your docker agent / slave. In that case we need to enable docker API on that host. 
    
## Installation
***
A little intro about the installation. 
```
$ git clone https://example.com
$ cd ../path/to/the/file
$ npm install
$ npm start
```
Note: To use the application in a special environment use ```lorem ipsum``` to start.

Provide instructions on how to collaborate with your project.
> Maybe you want to write a quote in this part. 
> Should it encompass several lines?
> This is how you do it.
 
  
  
I wanted to see myself -
Will be in a position to single handed deliver any requirement within Directory Services space. 
Able to deploy new DS services into cloud - EKS and complete data migration 
Help architecure team to come with the solution which is more efficient, robust and future oriented. 
Able to complete all mandatory learning and training on / before time. 
Have proper documentation and knowledge transfer aligned so that new member can be onboarded with minimal effort, and can be utilized quickly.

# How to create a separate node as the environment to act as jenkins agent ?
***
## Pre-requisite
* Node needs to have ssh connectivity, and within home directory of the user you need to create .ssh directory and need to copy public key into authorized_keys
* Below command will give you public and private key
```
ssh-keygen -b 2048 -t rsa
```
* private key you need to share with client, which they can use as an identity file (_ssh -i_)
* Now we are good to add node from UI
* You need java 8 or java 11 on system, make sure to access it from /usr/bin/java
```
Manage Jenkins -- Manage nodes and cloud -- New node -- Node name : whatever best suits and type : permanent agent 
In the second screen 
Name - whatever best suits you 
Description - whatever best suits you 
Number of executors : 2
Remote root directory : /apps/jenkins-agent
Label : uniquely identify node
Usage : use this node as much as possible 
Host : IP of node
Credentials : Add ssh private key in jenins system credentials 
Host Key Verification Strategy : Non verifying 
Availability : online as much as possible
```


