# [Deployment 2:Jenkins EC2 Instance Deployment]
  ###### August 23, 2023

### [Purpose:]

- To utilize the safest way to serve up a web browser by planning, coding, building and testing in a staging environment, and then building, testing and deploying my web application in the production environment
- To provision a Jenkins server through a newly created AWS EC2 instance with necessary protocols, permissions and downloaded applicaitons to successfully deploy web application. I previously used my instructor's Jenkins browser with the necessary plugins needed. Learning how to establish my Jenkins web browser and server give me admin access over my own Jenkins browser and the ability to customize plugins for staging my virtual environment. 

# [Description]

This project began diagramming the plan for my deployment in Draw.io including how I would use **GitHub**, **Jenkins**, and **AWS Elastic Beanstalk**. Github allowed me to create my own repository to store the application code and other files to test in Jenkins and deploy in AWS Elastic BeanstalkJenkins allowed me to create and test my deployment in a staging environment to ensure that it would return a 200 response from the server once deployed. Once my build passed the test phase in Jenkins, I created IAM roles and an EC2 instance through Elasticn Beanstalk. This allowed AWS access with the necessary permissions to update and launch my deployment through the IAM roles of **AWSElasticBeanstalkWebTier**, **AWSElasticBeanstalkMulticontainerDocker** and **AWSElasticBeanstalkWorkerTier**. After recieving a **Health status of Degraded**, I went into the Logs and found the issue in **/var/log/web.stdout.log** that showed the name of the application file containing my Python code was typed incorretly. Once I rectified the issue, Elastic Beanstalk was able to read my deployment properly. Finally, the EC2 instance created an applicable production environment to deploy my web applicaiton successfully. 

### [Github steps]
###### [Below you will find the necessary steps that I took to test and deploy my web applicaiton:]**

### [Jenkins steps]
###### [Below you will find the necessary steps that I took to test and deploy my web applicaiton:]**Steps:
1. Launch an EC2 with Jenkins installed and activated
Jenkins is the main tool used in this deployment for pulling the program from the GitHub repository, then building, testing, and deploying it to a server.
The Jenkins EC2 from previous deployments is used. It is on the default VPC that AWS provides

### [Elastic Beanstalk Steps]
###### [Below you will find the necessary steps that I took to test and deploy my web applicaiton:]**





# [Purpose of Deployment]

* To locate and rectify an issue in the code in order to deploy a web application using AWS Elastic Beanstalk.

# [Description]

This project began diagramming the plan for my deployment in Draw.io including how I would use **GitHub**, **Jenkins**, and **AWS Elastic Beanstalk**. I continued to plan and build within a previously created Jenkins account by my instructor. Jenkins allowed me to create and test my deployment in a staging environment to ensure that it would return a 200 response from the server once deployed. Once my build passed the test phase in Jenkins, I created IAM roles and an EC2 instance through Elasticn Beanstalk. This allowed AWS access with the necessary permissions to update and launch my deployment through the IAM roles of **AWSElasticBeanstalkWebTier**, **AWSElasticBeanstalkMulticontainerDocker** and **AWSElasticBeanstalkWorkerTier**. After recieving a **Health status of Degraded**, I went into the Logs and found the issue in **/var/log/web.stdout.log** that showed the name of the application file containing my Python code was typed incorretly. Once I rectified the issue, Elastic Beanstalk was able to read my deployment properly. Finally, the EC2 instance created an applicable production environment to deploy my web applicaiton successfully. 

###### [Below you will find the necessary steps that I took to test and deploy my web applicaiton:]**

1. Diagram the plan for deployment on Draw.io:
   
![Diagram of Deployment 1 1]

2. Log into GitHub account
3. Create new GitHub repository
4. Create **Documentation.md** file to record the staging and production environment of deployment
5. Open Kura Labs c4 Deployment-1 repository and follow the provided instructions
6. Press the **Code** tab and download files from Kura Labs repository
7. Unzip files by extracting Kura Lab files from the folder populated in your terminal in order for them to upload properly onto your GitHub repository 
8. Upload Kura Lab repository files into new GitHub repository created in **Step 3**
   

**9. [Create Build in Jenkins:]**


10. Sign into your Jenkins account
11. Press **New Item** tab to create new pipeline build
12. Name pipeline "First name, Last name initial"
13. Select Pipeline script from SCM
14. Choose Git in the dropdown from SCM
15. Go back to newly created GitHub repository and copy the HTTP code or URL of the repository
16. Paste code into "Repsitory line" in Jenkins
    

**17. [Create token for Jenkins using GitHub account:]**


18. Go back to your GitHub and press profile picture/icon
19. Select **Settings**-->**Developer Settings**-->**Personal Access Tokens**--> **Tokens(classic)**
20. Select **Generate new token**-->**Generate new token (classic)**-->Sign into GitHub if prompted
21. Create note description-->Select scopes: **repo** and **admin repo** to give full access to repository.
22. Click **Generate token**--> Copy and past link into **password line** in Jenkins
23. Continue on Jenkins-->Add token associated with repository--> Select main branch
24. Submit to generate build and select **Build Now** and pass staging environment in Jenkins 

[[Download GitHub Repository to unzip files and re-zip them to upload onto AWS Elastic Beanstalk]]

25. Create zip file folder in your File Explorer **[Windows OS]** to compress your GitHub repository. This new compressed zip file should not exceed 500 MB and should not include parent folder from your original repository to ensure that all characters in file are configured correctly in Elastic Beanstalk. You will need to extract files from the folder and create a new compressed zip file like in **Step 7**
26. Select files within the downloaded file of your repository and transfer them into a new compressed zip folder. This ensures that the files are zipped to Elastic Beanstalk's standards

[[After checking the console output responses and passing the test phase in Jenkins, you can go on to creating **IAM Roles** and the **Python Url Shortener** through **AWS Elastic Beanstalk**]]


**[27.Navigating throguh AWS Elastic Beanstalk]**


[Create **IAM Roles**]

28. Sign into AWS with appropriate Account ID, IAM user name, and password
    
29. Select **Roles** in Dashboard--> Click **Create role**--> Select **AWS service** for trusted entity type--> Under the dropdown for AWS Services: Select **Elastic Beanstalk**--> Select **Customizable** option under cases to give Elastic Beanstalk permission to manage AWS resources of your deployment--> Click **Next**--> Click **Next**--> Enter **AWS-Elasticbeanstalk-service-role** in Role name--> "Create Role
    
30. To create the second and third role: Click **Create Role**--> Select **AWS service** for trusted entity type--> Click **EC2** under common use cases--> Click Next--> Under Permission policies: Select **AWSElasticBeanstalkWebTier**, **AWSElasticBeanstalkMulticontainerDocker** and **AWSElasticBeanstalkWorkerTier**--> Click Next--> Enter **Elastic-EC2** in **Role name** field--> Click **Create Role**
    
[These roles allow the instances in your web server environment to access and upload necessare files and grants permissions for Amazon Elastic Container Service to organize and cluster task within container environments.]

[Create and deploy a **Python URL shortener**]

31. Select **Create Application**--> Name application **URL-shortener**--> Select **Python** in Platform dropdown--> Select **Python 3.9 running on 64bit Amazon Linux 2023** in Platform branch dropdown-->Select **Upload your code**--> Type **V1** in version label field--> [Choose and upload the compressed zip file of your repository]-->Click **Next**
32. Select **ElasticEC2** in EC2 instance profile dropdown--> Click **Next**--> Select default VPC in VPC dropdown--> Select **us-east-1a** availability zone--> Click **Next**--> Select **General Purpose (SSD)** in Root Volume type drop down--> Change the size field to 10GB-->Select **ONLY "T2.MICRO"** under **Instance Types** and **DESELECT** any other choices--> Click **Next**--> Click **Next**--> Click **Submit**
    
[The URL shortener reduces the number of characters in a URL so that it is easier for Elastic Beanstalk to read, remember, and share your web service and application. AWS Elastic Beanstalk makes it easier for developers to quickly depoly and manage these applications.]

33. **Upload and Deploy** your compressed zip file on Elastic Beanstalk. You will know that you passed once the **health status reads "OK"** and you get a response that your deployment has uploaded successfully to your EC2 instance.











Issues/Troubleshooting:
  My first attempt to create my Jenkins account, I skipped the option to create "Admin Username and Password". I was able to use upload my build but the build was unsuccessuful. After multiple attempts to test my pipeline, I realized I had to separately install the "Pipiline Utility Steps" plugin (instructions listed in Step #). I previously thought that this plugin was included in the suggested plugin installs. Once I installed the necessary plugin, I did a soft restart of my Jenkins browser and I was prompted to log back into my account. Upon trying to log back in, my Username and password was not recognized because I skipped the optionto create Admin credentials after entering my passcode found in my Jenkins EC2 instance. 
  In order to troubleshoot this issue, I had to create a new EC2 instance, with the installed SSH and Jenkins security group with Port 8080 and continue following steps #-# again in order to install and update the necessary applications. After this step, I found the passcode in /var///// and entered it into my new running browser with its new public IP address. Then I created my Admin credentials, installed the "Pipeline Utility Steps" plugin, uploaded my build, selected Continue under the "Packagaing.." phase of my pipleline and my pipeline was packed successfully. 
