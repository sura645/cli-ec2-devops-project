# 🚀 EC2 DevOps Project (AWS CLI)

## 📌 Project Overview

This project demonstrates a basic DevOps workflow using AWS CLI:

* Create an EC2 instance
* Connect via SSH
* Create a sample project
* Manage files inside EC2
* Document execution with screenshots

---

# 🧰 Prerequisites

* AWS CLI installed and configured
* AWS account
* Basic knowledge of terminal commands

---

# 📁 Project Structure

```bash id="z2g8yl"
my-devops-project/
│
├── app.js
├── Dockerfile
├── README.md
└── screenshots/
    ├── 1-aws-config.png
    ├── 2-create-ec2.png
    ├── 3-ssh-login.png
    ├── 4-project-files.png
```

---

# 📸 Screenshots

## 🔹 AWS CLI Configuration

![AWS Config](screenshots/1-aws-config.png)

## 🔹 EC2 Instance Creation

![EC2](screenshots/2-create-ec2.png)

## 🔹 SSH Login

![SSH](screenshots/3-ssh-login.png)

## 🔹 Project Files

![Files](screenshots/4-project-files.png)

---

# ⚙️ Step-by-Step Execution (AWS CLI)

## ✅ Step 1: Configure AWS CLI

```bash id="p1b9rr"
aws configure
```

👉 Provide:

* Access Key
* Secret Key
* Region: ap-south-1
* Output: json

---

## ✅ Step 2: Create Key Pair

```bash id="7fdavm"
aws ec2 create-key-pair \
--key-name my-key \
--query 'KeyMaterial' \
--output text > my-key.pem
```

```bash id="if7jbc"
chmod 400 my-key.pem
```

---

## ✅ Step 3: Create Security Group

```bash id="cqxja6"
aws ec2 create-security-group \
--group-name my-sg \
--description "My security group"
```

---

## ✅ Step 4: Allow SSH Access

```bash id="8g5c24"
aws ec2 authorize-security-group-ingress \
--group-id <GROUP_ID> \
--protocol tcp \
--port 22 \
--cidr 0.0.0.0/0
```

---

## ✅ Step 5: Launch EC2 Instance

```bash id="87nfjj"
aws ec2 run-instances \
--image-id ami-0f58b397bc5c1f2e8 \
--instance-type t2.micro \
--key-name my-key \
--security-group-ids <GROUP_ID>
```

---

## ✅ Step 6: Get Public IP

```bash id="m0dqdb"
aws ec2 describe-instances \
--instance-ids <INSTANCE_ID> \
--query 'Reservations[*].Instances[*].PublicIpAddress' \
--output text
```

---

## ✅ Step 7: Connect to EC2

```bash id="dqnoq9"
ssh -i my-key.pem ec2-user@<PUBLIC_IP>
```

---

## ✅ Step 8: Create Project Folder

```bash id="f0nh27"
mkdir my-devops-project
cd my-devops-project
```

---

## ✅ Step 9: Create Project Files

```bash id="k3yij0"
touch app.js Dockerfile README.md
```

### 📄 app.js

```javascript id="9ap28q"
console.log("Hello from EC2 DevOps Project!");
```

### 📄 Dockerfile

```dockerfile id="b1q2ab"
FROM node:18

WORKDIR /app

COPY . .

CMD ["node", "app.js"]
```

---

## ✅ Step 10: Create Screenshots Folder

```bash id="o1p8dz"
mkdir screenshots
```

👉 Store all execution screenshots inside this folder.

---

# 🎯 Learning Outcome

* AWS CLI usage for infrastructure
* EC2 instance provisioning
* SSH remote access
* Basic project setup in Linux
* Folder structure for real DevOps project