Jenkins EC2 Instance Deployment
8/23/23

Purpose:


Previously, applications were hosted on EC2's that were manually set up by instructor 
EC2 instance steps

Github steps

Jenkins steps
Steps:
1. Launch an EC2 with Jenkins installed and activated
Jenkins is the main tool used in this deployment for pulling the program from the GitHub repository, then building, testing, and deploying it to a server.
The Jenkins EC2 from previous deployments is used. It is on the default VPC that AWS provides

Elastic Beanstalk Steps


Issues/Troubleshooting:
  My first attempt to create my Jenkins account, I skipped the option to create "Admin Username and Password". I was able to use upload my build but the build was unsuccessuful. After multiple attempts to test my pipeline, I realized I had to separately install the "Pipiline Utility Steps" plugin (instructions listed in Step #). I previously thought that this plugin was included in the suggested plugin installs. Once I installed the necessary plugin, I did a soft restart of my Jenkins browser and I was prompted to log back into my account. Upon trying to log back in, my Username and password was not recognized because I skipped the optionto create Admin credentials after entering my passcode found in my Jenkins EC2 instance. 
  In order to troubleshoot this issue, I had to create a new EC2 instance, with the installed SSH and Jenkins security group with Port 8080 and continue following steps #-# again in order to install and update the necessary applications. After this step, I found the passcode in /var///// and entered it into my new running browser with its new public IP address. Then I created my Admin credentials, installed the "Pipeline Utility Steps" plugin, uploaded my build, selected Continue under the "Packagaing.." phase of my pipleline and my pipeline was packed successfully. 
