# Deployment 4 Utilizing Terraform
<p>
Utilizing Jenkins and Terraform to deploy a Flask app
</p>

## Purpose
<p>
Notice how when I did my last <a href="https://github.com/AdreReyes/Jenkins_deployment_3">deployment</a> it was manual. I manually went into my AWS Console and created a VPC, a subnet, and two EC2s. One for my Jenkins server and the other for my Jenkins agent all just to view my Flask application. Its a similar case this time where I created a VPC, subnet, EC2, etc in AWS but through the use of Terraform. All it takes is configuration of the "desired state" in Terraform files. If the last deployment was done manually then this deployment surely helps the user realize the resourcefulness of Terraform where AWS infrastructure can be spun up with code and built within seconds in a Jenkins pipeline. 
</p>

## Table of Contents

<a href="https://github.com/AdreReyes/Terraform_Deployment4/blob/main/Documentation.md"> - Documentation </a>

<a href="https://github.com/AdreReyes/Terraform_Deployment4/blob/main/Diagram_4.png"> - Diagram </a>

## Checklist
- Modify "test_app.py" if you wish to specify different unit tests for your application
- Ensure that the Terraform destroy stage is included in your Jenkinsfile and is in position BEFORE the apply stage to destroy your resources
  
## Link to Original Repo
<a href="https://github.com/kura-labs-org/kuralabs_deployment_4"> Original repo</a>


