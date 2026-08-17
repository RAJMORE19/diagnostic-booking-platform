**Wherever we work—local machine or anywhere else—we will start from the local machine and proceed step by step, mentioning everything here.**

**OUR MAIN WORKING MACHINE**

OS:        Ubuntu 24.04 LTS
Instance:  t3.medium
CPU:       2 vCPU
RAM:       4 GB
Storage:   30 GB gp3

**Installing Tools**

## Git ## → clone, manage, commit, and push project code to GitHub.

sudo apt update
sudo apt install git -y
git --version

### AWS CLI ### → connect to and manage AWS resources from the terminal. 

sudo apt update
sudo apt install awscli
aws configure
AWS Access Key ID: Your public API key. 
AWS Secret Access Key: Your private API key.
Default region name: Your primary operational region (e.g., us-east-1).
Default output format: How you want data returned (type json).

### TERRAFORM ### → create and manage our AWS infrastructure as code.
wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform
terraform -version


### kubectl ###→ manage and troubleshoot EKS/Kubernetes.

### Helm ### → install/manage Kubernetes applications and packages.

### Docker###  → build and test our microservice images before pushing to ECR.

### Trivy### → scan Docker images and code for security vulnerabilities.

