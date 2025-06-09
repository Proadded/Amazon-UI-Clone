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

