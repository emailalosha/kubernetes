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
 
  
