EC2 DevOps Project (AWS CLI Based)
📌 Project Overview

This project demonstrates how to:

Create an EC2 instance using AWS CLI
Connect to the instance via SSH
Create a simple Node.js app
Push the project to GitHub
⚙️ Prerequisites

Make sure you have:

AWS Account
AWS CLI installed
Git installed
Basic terminal knowledge
🧭 Step 1: Configure AWS CLI
aws configure

Provide:

AWS Access Key ID: <your-key>
AWS Secret Access Key: <your-secret>
Region: ap-south-1
Output: json
🖥️ Step 2: Create Key Pair
aws ec2 create-key-pair \
    --key-name my-key \
    --query 'KeyMaterial' \
    --output text > my-key.pem

👉 This creates a private key file to connect to EC2.

Secure it:

chmod 400 my-key.pem
🔐 Step 3: Create Security Group
aws ec2 create-security-group \
    --group-name my-sg \
    --description "My security group"

👉 Copy the GroupId from output.

🌐 Step 4: Allow SSH Access
aws ec2 authorize-security-group-ingress \
    --group-id <GROUP_ID> \
    --protocol tcp \
    --port 22 \
    --cidr 0.0.0.0/0

👉 Opens port 22 for SSH access.

🚀 Step 5: Launch EC2 Instance
aws ec2 run-instances \
    --image-id ami-0f58b397bc5c1f2e8 \
    --count 1 \
    --instance-type t2.micro \
    --key-name my-key \
    --security-group-ids <GROUP_ID>

👉 Copy the InstanceId.

🌍 Step 6: Get Public IP
aws ec2 describe-instances \
    --instance-ids <INSTANCE_ID> \
    --query 'Reservations[*].Instances[*].PublicIpAddress' \
    --output text
🔑 Step 7: Connect to EC2
ssh -i my-key.pem ec2-user@<PUBLIC_IP>
📁 Step 8: Create Project Folder
mkdir my-devops-project
cd my-devops-project
📄 Step 9: Create Project Files
touch app.js Dockerfile README.md
🧾 app.js
console.log("Hello from EC2 DevOps Project!");
🐳 Dockerfile
FROM node:18

WORKDIR /app

COPY . .

CMD ["node", "app.js"]
📝 Step 10: Install Git
sudo yum install git -y
⚙️ Step 11: Configure Git
git config --global user.name "your-name"
git config --global user.email "your-email"
📦 Step 12: Initialize Git Repo
git init
➕ Step 13: Add Files
git add .
💾 Step 14: Commit Code
git commit -m "Initial commit - EC2 project"
🌐 Step 15: Connect to GitHub

Create a repository in GitHub, then:

git remote add origin https://github.com/<username>/ec2-devops-project.git
🚀 Step 16: Push Code
git branch -M main
git push -u origin main
📁 Project Structure
my-devops-project/
│
├── app.js
├── Dockerfile
└── README.md