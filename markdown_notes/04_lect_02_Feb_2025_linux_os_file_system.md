# **Linux OS and File System - Class 03 Notes**

## **What is an Operating System?**

An Operating System (OS) acts as an intermediary between the user and the machine (computer). It allows users to communicate with the computer using commands and interfaces.

### **Key Points:**

- An OS allows execution of applications and system software on a computer.
- It plays a vital role in managing hardware resources and providing user interaction.
- Some of the dominant OS in the market include:
  - **Linux**
  - **Windows**
  - **Mac OS**
  - **Android**
  - **iOS**

## **Windows OS (Microsoft)**

- **GUI-Based (Graphical User Interface)**
- **User-Friendly** (Easy to operate)
- **Single-User Based OS**
- **Paid OS (Commercial Software)**
- **Lower Security** (Requires antivirus software)
- **Preferred for personal use**
- **Not Recommended for Serious Application Deployment** (Business use cases prefer Linux)

## **Linux OS**

- Created by **Linus Torvalds** as an alternative to Unix.
- Unix developers did not accept his suggestions, so he created his own OS.
- Inspired by **Minix OS**, he developed **Linux**, which became **Linux OS**.
- **Free and Open Source**

## **Multi-User OS Features in Linux**

- Provides **high security**
- Highly recommended for **applications and project operations**
- **CLI-Based (Command Line Interface)**

### **Setting Up Linux for Projects**

Linux OS is commonly used for setting up **software infrastructure**. Some popular Linux distributions include:

- **Red Hat Linux**
- **Amazon Linux**
- **Ubuntu Linux**
- **SUSE Linux**
- **Fedora Linux**
- Over **200+ Linux distributions** are available.

### **Linux Distributions (Flavors)**

- Linus Torvalds made Linux **free and open-source**.
- Large companies modified Linux to fit their needs and rebranded it.
- Examples:
  - **Amazon Linux**
  - **Ubuntu Linux**
  - **Red Hat Linux (RHEL)**
  - **Kali Linux**
## **OS & Why We Need It?**

- **Windows OS** ➝ Uses a **Virtual Machine**
- **Linux OS** ➝ Uses a **Virtual Machine**

### **Using AWS for Linux OS**

- AWS (Amazon Web Services) provides a cloud-based Linux environment.
- AWS offers **750 free hours** yearly (24x30 = **720 hours/month**).
- You can create and manage Linux virtual machines on **AWS EC2 instances**.

#### **How to Create AWS Account & Setup EC2 Instance?**

1. [How to create AWS account](https://github.com/hacker123shiva/DevOps-with-AWS/blob/main/markdown_notes/how_to_create_aws.md)
2. [How to create EC2 and use with MobaXterm](https://github.com/hacker123shiva/DevOps-with-AWS/blob/main/markdown_notes/How_to_use_ec2.md)

## **Creating a Linux Virtual Machine on AWS**

- **Steps to create a Linux instance on AWS EC2:**
  - Login to AWS account
  - Create a **Linux Virtual Machine**
  - Use **SSH Protocol** to connect
  - Connect using **MobaXterm** or another terminal

Diagram Representation:

```
Windows OS  --->   SSH Protocol  --->  AWS EC2 Linux Instance
```

## **Linux File System**

### **Everything in Linux is Represented as a File**

- **Ordinary Files** (Start with `-`)
- **Directories (Folders)** (Start with `d`)
- **Link Files** (Start with `l`)

### **Basic Linux Commands**

#### **Directory Management**

- Create a Directory:
  ```bash
  mkdir <directory-name>   # Example: mkdir devops
  ```
- Delete an Empty Directory:
  ```bash
  rmdir <directory-name>   # Example: rmdir devops
  ```
- Change Directory:
  ```bash
  cd <directory-name>  # Example: cd devops
  ```
- Exit a Directory:
  ```bash
  cd ..
  ```

#### **File Management**

- Create a Normal File:
  ```bash
  touch <file-name>  # Example: touch telusko.txt alien.txt
  ```

#### **List Files in a Directory**

- List all files:
  ```bash
  ls
  ```
- List files in **alphabetical order (A-Z)**:
  ```bash
  ls -l
  ```
- List files in **reverse alphabetical order (Z-A)**:
  ```bash
  ls -lr
  ```
- List files **sorted by latest modification time**:
  ```bash
  ls -lt
  ```
- List **old files first**:
  ```bash
  ls -ltr
  ```
