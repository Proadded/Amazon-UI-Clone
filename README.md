# 🚀 Amazon UI Clone Deployment with AWS EC2, Docker & Jenkins

This repository documents the automated deployment of a static HTML/CSS Amazon UI clone using AWS EC2, Docker and Jenkins CI/CD.

---

## 📋 What You’ll Find in This README
1. EC2 setup & SSH access
2. Docker installation & container setup
3. Jenkins installation from official repository
4. CI/CD pipeline configuration screenshots
5. Errors encountered and fixes applied

---

## 🧠 1. EC2 Setup & SSH Access

- EC2 instance launched with Ubuntu 22.04, `t2.micro` type, Elastic IP assigned.
- SSH access tested via MINGW64/Git Bash:
  ```bash
  ssh -i "C:/Users/Aditya/Desktop/aditya-key.pem" ubuntu@<ec2-ip>

✅ Fixed path errors & permission denied via chmod on PEM file 
![DEVOPS7](https://github.com/user-attachments/assets/32654e72-909d-4c15-80cc-83f594b05dad)

---

## 🐋 2. Docker Installation & Static Site Container

Installed Docker:
sudo apt update && sudo apt install docker.io -y

![DEVOPS8](https://github.com/user-attachments/assets/90bb50e3-3afd-470d-a25f-5652e1e4100a)

Built Dockerfile:
FROM nginx:alpine
COPY . /usr/share/nginx/html

Built and ran the container:
docker build -t amazon-ui-clone .
docker run -d -p 80:80 amazon-ui-clone

✅ Static site live

![DEVOPS5](https://github.com/user-attachments/assets/052db86a-f6ef-46f1-a391-aad773c39e8f)

---

## 🛠️ 3. Jenkins Installation

Installed Java:
sudo apt install openjdk-17-jdk -y\

Added Jenkins repo & key, then installed Jenkins:
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
echo deb http://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list
sudo apt update
sudo apt install jenkins -y
sudo systemctl start jenkins
sudo systemctl enable jenkins

🔴 Error encountered: GPG error: public key NO_PUBKEY 

![DEVOPS9](https://github.com/user-attachments/assets/76efcb1d-e0fa-4902-aad6-2b07cd6e7bf7)

— resolved by fetching and adding the Jenkins repo key manually before install.

✅ Installation succeeded 

![DEVOPS10](https://github.com/user-attachments/assets/3308ae00-7572-4b8b-8178-70afec36600f)

---

## 🔄 4. Jenkins CI/CD Pipeline Configuration

Created a Pipeline job in Jenkins.
Enabled GitHub Project and entered repo URL.
Configured Build Triggers: GitHub webhooks + Poll SCM.

Shell Build Step used:
docker stop $(docker ps -aq) || true
docker rm $(docker ps -aq) || true
docker rmi amazon-ui || true
docker build -t amazon-ui .
docker run -d -p 80:80 amazon-ui

📸 Console output screenshot DEVOPS1.jpg shows successful container rollout.

🧩 UI of Jenkins build step configuration in 

![DEVOPS3](https://github.com/user-attachments/assets/912d5657-5841-4131-84d0-72beacf566df)


✅ Build #4 success screenshot

![DEVOPS2](https://github.com/user-attachments/assets/225cf25d-a765-4975-a4de-5680f40fd66b)

project status page in 

![DEVOPS4](https://github.com/user-attachments/assets/00284dec-6dd6-4a47-b0d9-477682e598c5)

---

## ⚠️ 5. Common Errors & Fixes
| Issue                            | Description & Fix                                  |
| -------------------------------- | -------------------------------------------------- |
| **PEM path errors**              | Used `chmod 400` and corrected path in Git Bash    |
| **Docker access denied**         | Added user to Docker group and reconnected session |
| **Jenkins `NO_PUBKEY`**          | Added Jenkins GPG key manually before apt install  |
| **`docker stop` argument error** | Included \`                                        |

---

## 👇 6. How to Use

1.Clone this repo on EC2 or local system.

2.Build & run Docker container:
  docker build -t amazon-ui .
  docker run -d -p 80:80 amazon-ui

3.Jenkins (if installed): configure webhook, then builds will auto-trigger and redeploy your static UI clone.


## 👨‍💻 Author
## Aditya Verma


