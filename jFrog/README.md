# Jfrog as package manager and docker image repository


## Login to *https://jfrog.com/start-free/* and register yourself
### You need to select cloud provider, cloud region and unique environment name. Mine is *reedauthorized.jfrog.io*
### After registration you will get email from jFrog to verify, verify your email and login to your environment ( *reedauthorized.jfrog.io*) using the creds provided at time of register
#
#
#

### Now this is the time to access *https://my.jfrog.com/* and register yourself to manage your cloud subscription
### First time login to - https://my.jfrog.com/ , click on forgot password. Provide your email (the one provided at cloud subscription) it will send a link to your email. Register by clicking the email sent by jFrog. Finally put password and login to https://my.jfrog.com/. Here you can see your cloud subscription for jFrog


#### On left hand side you will see two tab, one for administrator and other for aapplications. Administrator can create repository, and manage other settings. 

    Adminstrations -- Artifactory -- General -- Settings (To manage file upload settings and all)
   #
     Adminstrations -- Repositories -- repositories -- on right hand side
     create create local  repo (select generic, incase you want to manage files or folders) 
     
   #
     Adminstrations -- Repositories -- repositories -- on right hand side
     create create local  repo (select docker, incase you want to manage docker images) 
     
   #
     Adminstrations -- Repositories -- repositories -- on right hand side
     create create remote  repo (select docker, incase you want to manage docker images and on some  remote loc. 
     go for default incase you dont have much info) 
     
   #
     Adminstrations -- Repositories -- repositories -- on right hand side
     create create virtual  repo (select docker, put local first and remote next, also default repo should be local only) 
     
   #
    Adminstrations -- Artifactory -- Import and Export -- 
    Upload files in selected repository (Make sure to zip file on top of zip so that zip file will be available on artifactory)




