### Jenkins Basic ###

This is how you can run Jenkins as docker container. 

  docker run --name jenkins-docker -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home -d jenkins/jenkins:lts-jdk11
  
Above command execution is going to give us Jenkin master or controller. This would be enough to write and execute our pipeline jobs. However, for a team if they wanted to execute something concurrently we may need to have jenkins nodes acting as agent or slave, where actual execution going to happen. 

With great supportability from Jenkins, now we are able to spin up ephemeral docker slave or agent which can be live / or start based on on-demand basis. 

 
  
