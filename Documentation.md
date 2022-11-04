# Deployment 4 Documentation 
 <p> Successfully deployed a Flask application utilizing Terraform </p>
 
<h2> Install Jenkins on an EC2 </h2>

*	I already have an EC2 set up with Jenkins installed on it. The instance has ports 8080, 22, and 80 open on it. 

<img width="401" alt="image" src="https://user-images.githubusercontent.com/108366142/199889771-b8068bc7-3bca-43d4-ba42-5a61ba74c386.png">

*	It's set up with my default VPC and subnet. 

<img width="372" alt="image" src="https://user-images.githubusercontent.com/108366142/199890001-3fa9b5aa-a048-4af1-83f0-5051c00df937.png">

* Start the instance and connect to it.

<img width="423" alt="image" src="https://user-images.githubusercontent.com/108366142/199890105-56db46c4-8e4f-4e58-bd67-d841ead78985.png">

*	I ran the command <sudo systemctl status Jenkins> to check if my Jenkins server is running. 
  
<img width="468" alt="image" src="https://user-images.githubusercontent.com/108366142/199971507-f4cb567a-8eb7-41bf-87a1-043eb889160a.png">

<h2> Install Terraform on the Jenkins Server </h2>
  
* I went to this link for the directions on how to install Terraform on my Jenkins server: https://www.terraform.io/downloads. I ran each of the commands manually in my Jenkins server EC2 terminal.
  
<img width="420" alt="image" src="https://user-images.githubusercontent.com/108366142/199971900-5cefa8cb-35ff-4072-8dda-9f41fd7453a9.png">

* During the last command I got the message that the Terraform package will be installed.
  
<img width="370" alt="image" src="https://user-images.githubusercontent.com/108366142/199972355-8e2bb97d-f083-423d-b834-b9242253aeaa.png">

I made sure to run the command below to update my system. 
  
```
  sudo apt update
```
  
<h2> Configure credentials on Jenkins </h2>
  
* I accessed the Jenkins web server by running the command: <my_public_ip_address:open_port>. 
  
<img width="425" alt="image" src="https://user-images.githubusercontent.com/108366142/199974457-e55cd9da-ab08-4b5f-9e28-f089cc085011.png">

* Jenkins sign in page pops up!
  
<img width="468" alt="image" src="https://user-images.githubusercontent.com/108366142/199974588-ebdcf6df-fefc-4303-a2fd-671c0cfd2a36.png">

* Once signed in I selected “manage Jenkins” from menu on left side on the screen.
  
<img width="387" alt="image" src="https://user-images.githubusercontent.com/108366142/199974704-73d7c19e-b124-42ad-83bc-bf755dcb0825.png">

* Select manage credentials.
  
<img width="389" alt="image" src="https://user-images.githubusercontent.com/108366142/199976076-05aa4692-93ea-4c4a-af15-985cf495d4ba.png">

* At the bottom of the page I selected “global”.
  
<img width="461" alt="image" src="https://user-images.githubusercontent.com/108366142/199976284-43b6f611-3aed-4074-b9c3-596ed4138bf4.png">

* I selected “Add Credentials” from the left side of the screen.
  
<img width="395" alt="image" src="https://user-images.githubusercontent.com/108366142/199976420-c6b554f5-2900-4648-b0fa-17a3feb86c87.png">

* Under “New Credentials” I added new credentials that contained my AWS access key and selected create when done.

<img width="379" alt="image" src="https://user-images.githubusercontent.com/108366142/199978588-337081bb-5d56-4ee2-a424-22712f3e718a.png">

* Under “New Credentials” I added new credentials that contained my AWS secret key and selected create when done. 
  
<img width="397" alt="image" src="https://user-images.githubusercontent.com/108366142/199978746-647ebf7e-aaad-4f99-9244-795774abee52.png">

<h2> Create a Pipeline Build in Jenkins </h2>
  
* So, I have my Jenkinsfile here in Github which contains the steps to install pip, terraform, and all of the dependencies needed to build, apply, and deploy the Flask application via Terraform on a different EC2 machine rather than the one my Jenkins server is running on. 
  
<a href="https://github.com/AdreReyes/kuralabs_deployment_4/blob/main/Jenkinsfile">Jenkinsfile</a>
  
* Now I went into Jenkins and I downloaded the Jenkins plugin “Pipeline Keep Running” by selecting “manage Jenkins” from the left side of the screen >> manage plugins >> type Pipeline Keep Running in the empty text box >> select the plugin >> installed it. A check mark means it was installed successfully.
  
<img width="367" alt="image" src="https://user-images.githubusercontent.com/108366142/200033405-83749848-b991-4471-8a0c-d06db489a455.png">
  
<img width="418" alt="image" src="https://user-images.githubusercontent.com/108366142/200033947-ad300382-c83c-4ed9-a2f8-e544a0fa72d0.png">
  
<img width="324" alt="image" src="https://user-images.githubusercontent.com/108366142/200036115-f78e494a-2bab-4333-9bb4-210473eb5964.png">

* Now, to build the pipeline, I go back to the dashboard and select New item from the Dashboard.
  
<img width="228" alt="image" src="https://user-images.githubusercontent.com/108366142/200036877-7705d690-c31b-4b7f-90d8-50818e5e06a8.png">

* I want to build a multibranch pipeline so that’s what I select. 
  
<img width="311" alt="image" src="https://user-images.githubusercontent.com/108366142/200037099-38ace8a0-c641-486c-a6f9-cf6e319f4793.png">

*	I enter a display name, description, and choose Github for the branch source because I want to connect my Gitub repo to Jenkins so it can build the application. 
  
<img width="418" alt="image" src="https://user-images.githubusercontent.com/108366142/200037964-2de902bb-5e48-41ae-a001-cec6065c2b52.png">

* After my credentials came out okay after adding the HTTP link while setting up the pipeline I chose Save and Apply. I then see that the pipeline is building.
  
<img width="325" alt="image" src="https://user-images.githubusercontent.com/108366142/200038108-a4fba347-75b3-45b8-b1c4-9c317d72201f.png">

* After my credentials came out okay after adding the HTTP link while setting up the pipeline I chose Save and Apply. I then see that the pipeline is building. 
  
<img width="325" alt="image" src="https://user-images.githubusercontent.com/108366142/200038155-67d66a75-de50-4245-b114-07bee719984f.png">
  
The build was successful the third time. Errors will be reported at the end of the documentation.

<img width="321" alt="image" src="https://user-images.githubusercontent.com/108366142/200038418-fd3c7270-816f-4cd6-bd9f-2f8f2c7ea4bd.png">
  
The resources were created and now its time to destroy them. 

<img width="468" alt="image" src="https://user-images.githubusercontent.com/108366142/200039047-172ca022-aae7-4e9a-bb35-20963982c061.png">

* Now I added a Destroy stage to my Jenkinsfile at the very end so that these resources can be taken down last via Jenkins. 
  
<img width="468" alt="image" src="https://user-images.githubusercontent.com/108366142/200039868-8c1bb1c5-a813-4e0a-b2a8-681f1325871e.png">

<h2> Create a VPC with Terraform and Deploy Application to It </h2>
  
* I have a folder named intTerraform with the following files in it:
  * <a href="https://github.com/AdreReyes/kuralabs_deployment_4/blob/main/intTerraform/SG.tf">SG.tf</a> = holds my security groups
  * <a href="https://github.com/AdreReyes/kuralabs_deployment_4/blob/main/intTerraform/deploy.sh">deploy.sh</a> = file of dependencies and packages that will be installed to run Flask app on Gunicorn via port 8000 
  * <a href="https://github.com/AdreReyes/kuralabs_deployment_4/blob/main/intTerraform/main.tf">main.tf</a> = the configurations for Terraform to create resources in AWS 

* The resources I created via Terrafom was 1 VPC, an internet gateway, custom route table, and 1 public subnet that has 1 EC2 instance within 1 avaialability zone. My EC2 called “Webserver001” was created via the intTerraform main.tf file which is where I will use its public IP to check if the Flask application is running on port 8000.
  
<img width="468" alt="image" src="https://user-images.githubusercontent.com/108366142/200045679-01efd03f-ba17-429d-98a1-9f1c5c3267f5.png">
  
* The application was running so the deployment was successful!
  
  <img width="418" alt="image" src="https://user-images.githubusercontent.com/108366142/200046095-94e99b48-108d-4f53-b838-4de6bab269b1.png">
  
* The last step is to destroy the resources which means adding that Destroy stage back in the Jenkinsfile. 
  
```
  stage('Destroy') {
       steps {
        withCredentials([string(credentialsId: 'AWS_ACCESS_KEY', variable: 'aws_access_key'),
                        string(credentialsId: 'AWS_SECRET_KEY', variable: 'aws_secret_key')]) {
                            dir('intTerraform') {
                              sh 'terraform destroy -auto-approve -var="aws_access_key=$aws_access_key"
-var="aws_secret_key=$aws_secret_key"'
} }
}
```
 
* I go back in Jenkins and create the build with the destroy stage added. 
  
<img width="468" alt="image" src="https://user-images.githubusercontent.com/108366142/200046829-4d2c3787-aa87-4667-9fc0-3a770324a9ce.png">

* I go back and check if my resources have been destroyed and I can see that my EC2 has been terminated.
  
<img width="468" alt="image" src="https://user-images.githubusercontent.com/108366142/200046978-a2eebc18-b203-4393-855a-14b831002333.png">


  

 
  
