# [Deployment 2:Jenkins EC2 Instance Deployment]
  ###### August 23, 2023

### [Purpose:]

- To provision a Jenkins server through a newly created AWS EC2 instance with necessary protocols, permissions and downloaded applicaitons to successfully deploy web application. I previously used my instructor's Jenkins browser with the necessary plugins needed along with a previously launched EC2 inctance with necessary downloads. Establishing my own Jenkins web browser and server gives me admin access over my own Jenkins browser and the ability to customize plugins for staging my virtual environment. Creating and launching my own EC2 instance also provides me the ability to customize my own instance with the necessary security groups to establish SSH protocols for remote access between my EC2 and Jenkins web server, as well as HTTP protocols so that AWS can use its resources to unecrypt my web application for deployment through my public IP address from my EC2 instance. Learning these fundamental steps gives me practice in how to start the steps in procurring my CICD pipeline for automating and scaling my deployment process in the future. Ensuring my skills to build to my staging environment will help me ensure that my deployment is tested properly to ensure high quality user experience, adequate server connection, and shows me the safest way to make sure that my web applications and servers will be ready before deployment for my future production environments.

### [Description]

This project began diagramming the plan for my deployment in Draw.io including how I would use **GitHub**, **Jenkins**, and **AWS Elastic Beanstalk**. I continued to plan and build within a previously created Jenkins account by my instructor. Jenkins allowed me to create and test my deployment in a staging environment to ensure that it would return a 200 response from the server once deployed. Once my build passed the test phase in Jenkins, I created IAM roles and an EC2 instance through Elasticn Beanstalk. This allowed AWS access with the necessary permissions to update and launch my deployment through the IAM roles of **AWSElasticBeanstalkWebTier**, **AWSElasticBeanstalkMulticontainerDocker** and **AWSElasticBeanstalkWorkerTier**. After recieving a **Health status of Degraded**, I went into the Logs and found the issue in **/var/log/web.stdout.log** that showed the name of the application file containing my Python code was typed incorretly. Once I rectified the issue, Elastic Beanstalk was able to read my deployment properly. Finally, the EC2 instance created an applicable production environment to deploy my web applicaiton successfully. 

###### [Below you will find the necessary steps that I took to provision my own Jenkins server for my staging environment and to provosion my production environment to deploy my web applicaiton:]** 

### **[Plan & Code]**

1. Diagram the plan for deployment on Draw.io:

![Plan][https://github.com/DANNYDEE93/Deployment2/blob/main/Images%20of%20Deployment%202/Plan%20for%20deployment%202.jpg]
   
2. Log into GitHub account
3. Create new GitHub repository
4. Create **Documentation.md** file to record the staging and production environment of deployment
5. Open Kura Labs c4 Deployment-1 repository and follow the provided instructions
6. Press the **Code** tab and download files from Kura Labs repository
7. Unzip files by extracting Kura Lab files from the folder populated in your terminal in order for them to upload properly onto your GitHub repository 
8. Upload Kura Lab repository files into new GitHub repository created in **Step 3**

### **[BUILD & TEST]**
   
**9. [Create Build in Jenkins:]**

[Launch an EC2 with the necessary protocols to connect to my establish Jenkins server and web browser to provide me with admin access to utiilize my Jenkins account on my own]

1. Press **Instances** in the Dashboard --> Press **Launch Instance** button--> Name web server --> Select **Ubuntu** for OS --> Select **t2.micro** --> Select suggested key pair --> Select security groups that include: Port 22, 80 & 8080 under "Network Settings" (selected exisitng group with these protocols) --> Press **Launch Instance**

[Jenkins is the main tool used in this deployment for pulling the program from the GitHub repository, then building, testing, and deploying it to a server.]  

2. Within my EC2 instance: Download newest version of Python and Jenkins --> Copy and Paste ip address of EC2 and add port 80 to access web browser with Jenkins.
3. The web browser will show the location of admin passwrd --> Go back to EC2 and type "sudo cat /var/lib/jenkins/secrets/initialAdminPassword"

   ![https://github.com/DANNYDEE93/Deployment2/blob/main/Images%20of%20Deployment%202/sudo%20cat%20admin%20psswrd.png]

5. Copy and paste admin password into Jenkins browser--> Create admin account-->Install suggested plugins --> Go to **Available plugins** in the settings--> Install **Pipeline Utility Steps** --> Soft restart the browser --> Sign back into Jenkins account
   
    ! [https://github.com/DANNYDEE93/Deployment2/blob/main/Images%20of%20Deployment%202/Download%20plugins%20for%20environment.png]
   
5. Press **New Item** tab to create new pipeline build --> Name pipeline "First name, Last name initial" --> Select Pipeline script from SCM --> Choose Git in the dropdown from SCM --> Go back to newly created GitHub repository and copy the HTTP code or URL of the repository --> Paste code into "Repsitory line" in Jenkins

**6. [Create token for Jenkins using GitHub account:]**

7. Go back to your GitHub and press profile picture/icon
8. Select **Settings**-->**Developer Settings**-->**Personal Access Tokens**--> **Tokens(classic)**
9. Select **Generate new token**-->**Generate new token (classic)**-->Sign into GitHub if prompted
10. Create note description-->Select scopes: **repo** and **admin repo** to give full access to repository.
11. Click **Generate token**--> Copy and past link into **password line** in Jenkins
12. Continue on Jenkins-->Add token associated with repository--> Select main branch
13. Submit to generate build and select **Build Now** and pass staging environment in Jenkins

### **[MERGE]**

[[Download GitHub Repository to unzip files and re-zip them to upload onto AWS Elastic Beanstalk]]

14. Create zip file folder in your File Explorer **[Windows OS]** to compress your GitHub repository. This new compressed zip file should not exceed 500 MB and should not include parent folder from your original repository to ensure that all characters in file are configured correctly in Elastic Beanstalk. You will need to extract files from the folder and create a new compressed zip file like in **Step 7**
15. Select files within the downloaded file of your repository and transfer them into a new compressed zip folder. This ensures that the files are zipped to Elastic Beanstalk's standards.

[Check console output responses and check the phases of testing and passing the staging environment.]

16. For theis deployment, there was an included packaging/zip command within my applicaion code that compressed my GitHub file. Under the packaging phase in the console output, the location of the file within the EC2 home directory was given:

17. ![https://github.com/DANNYDEE93/Deployment2/blob/main/Images%20of%20Deployment%202/Jenkins%20compressed%20file%20location%20.png]

[Locating the file and unzipping the package makes it easily readable and you can make sure that it waas properly packaged]

18. Go back to EC2 and **cd /var/lib/jenkins/workspace/Deployment2/build/1.0.0.1.zip**
19. Download unzip: **sudo apt unzip** --> then use the "unzip" command on the "1.0.0.1.zip" file

20. ! [https://github.com/DANNYDEE93/Deployment2/blob/main/Images%20of%20Deployment%202/Jenkins%20compressed%20zip%20file_2.png]


[[After checking the console output responses and passing the test phase in Jenkins, you can go on to creating **IAM Roles** and the **Python Url Shortener** through **AWS Elastic Beanstalk**]]

### **[BUILD, TEST, DEPLOY]**

**[21.Navigating throguh AWS Elastic Beanstalk]**


[Create **IAM Roles**]

22. Sign into AWS with appropriate Account ID, IAM user name, and password
    
23. Select **Roles** in Dashboard--> Click **Create role**--> Select **AWS service** for trusted entity type--> Under the dropdown for AWS Services: Select **Elastic Beanstalk**--> Select **Customizable** option under cases to give Elastic Beanstalk permission to manage AWS resources of your deployment--> Click **Next**--> Click **Next**--> Enter **AWS-Elasticbeanstalk-service-role** in Role name--> "Create Role
    
24. To create the second and third role: Click **Create Role**--> Select **AWS service** for trusted entity type--> Click **EC2** under common use cases--> Click Next--> Under Permission policies: Select **AWSElasticBeanstalkWebTier**, **AWSElasticBeanstalkMulticontainerDocker** and **AWSElasticBeanstalkWorkerTier**--> Click Next--> Enter **Elastic-EC2** in **Role name** field--> Click **Create Role**
    
[These roles allow the instances in your web server environment to access and upload necessare files and grants permissions for Amazon Elastic Container Service to organize and cluster task within container environments.]

[Create and deploy a **Python URL shortener**]

25. Select **Create Application**--> Name application **URL-shortener**--> Select **Python** in Platform dropdown--> Select **Python 3.9 running on 64bit Amazon Linux 2023** in Platform branch dropdown-->Select **Upload your code**--> Type **V1** in version label field--> [Choose and upload the compressed zip file of your repository]-->Click **Next**
26. Select **ElasticEC2** in EC2 instance profile dropdown--> Click **Next**--> Select default VPC in VPC dropdown--> Select **us-east-1a** availability zone--> Click **Next**--> Select **General Purpose (SSD)** in Root Volume type drop down--> Change the size field to 10GB-->Select **ONLY "T2.MICRO"** under **Instance Types** and **DESELECT** any other choices--> Click **Next**--> Click **Next**--> Click **Submit**
    
[The URL shortener reduces the number of characters in a URL so that it is easier for Elastic Beanstalk to read, remember, and share your web service and application. AWS Elastic Beanstalk makes it easier for developers to quickly depoly and manage these applications.]

27. **Upload and Deploy** your compressed zip file on Elastic Beanstalk. You will know that you passed once the **health status reads "OK"** and you get a response that your deployment has uploaded successfully to your EC2 instance.


##### Issues/Troubleshooting:
  My first attempt to create my Jenkins account, I skipped the option to create "Admin Username and Password". I was able to use upload my build but the build was unsuccessuful. In order to troubleshoot this issue, I had to create a new EC2 instance, with the installed SSH and Jenkins security group with Port 8080 and continue following steps **Steps 29-54** again in order to install and update the necessary applications. 
