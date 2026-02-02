

## ****Infrastructure as Code (IaC) with Terraform – AWS Node.js + MySQL**

![Terraform](https://img.shields.io/badge/Terraform-IaC-blueviolet)
![AWS](https://img.shields.io/badge/AWS-Cloud-orange)
![Node.js](https://img.shields.io/badge/Node.js-Backend-green)
![MySQL](https://img.shields.io/badge/MySQL-Database-blue)


## Project Overview

This project demonstrates how to use **Terraform** to provision and manage a complete **AWS infrastructure** for a Node.js application using **Infrastructure as Code (IaC)** principles.

The entire infrastructure  including compute, database, storage, networking, and security is defined in Terraform configuration files, enabling **automation, consistency, and repeatability**.



##  Architecture Overview

The application is deployed on AWS using the following architecture:

```
User
  |
  |  HTTP (Port 3000)
  v
Amazon EC2 (Node.js App)
  |
  |  MySQL (Port 3306)
  v
Amazon RDS (MySQL 8.0)

Amazon S3
(Static Images)
```

### Architecture Diagram

<img width="960" height="610" alt="image" src="https://github.com/user-attachments/assets/e17ec7a9-a1e4-48e8-9577-edbffa6d3b70" />



## AWS Services Used

### 1.Amazon EC2

* Instance Type: `t3.micro`
* OS: Ubuntu (AMI)
* Hosts the **Node.js application**
* Automatically bootstrapped using **user_data**:

  * Clones GitHub repository
  * Installs Node.js & npm
  * Configures environment variables
  * Installs dependencies

### 2️. Amazon RDS (MySQL)

* Engine: MySQL 8.0
* Instance Class: `db.t3.micro`
* Allocated Storage: 10 GB
* Database Name: `dinethdb`
* Secure access restricted via Security Groups
* Endpoint dynamically passed to EC2 using Terraform outputs

### 3️.Amazon S3

* Stores static image assets
* Files uploaded automatically using Terraform `aws_s3_object`
* Used by the Node.js application

### 4️.AWS VPC & Security Groups

#### EC2 Security Group

* SSH access: Port `22`
* Application access: Port `3000`
* Inbound traffic allowed from all IPs (for demo purposes)

#### RDS Security Group

* MySQL access: Port `3306`
* Restricted to EC2 security group and specific IP


## Terraform Components

### Key Terraform Resources

* `aws_instance` – EC2 instance
* `aws_db_instance` – RDS MySQL database
* `aws_s3_bucket` & `aws_s3_object` – S3 storage and objects
* `aws_security_group` – Network security
* `locals` & `outputs` – Dynamic configuration sharing

### Terraform Outputs

* RDS Endpoint
* Database Name
* Database Username
* EC2 Public IP

These outputs are used to automatically configure the application environment.



## Deployment Steps

1. Clone the repository:

```bash
git clone https://github.com/dineth28-max/Infrastructure-as-code-with-terraform.git
```

2. Initialize Terraform:

```bash
terraform init
```

3. Validate the configuration:

```bash
terraform validate
```

4. Apply the infrastructure:

```bash
terraform apply
```

5. Access the application:

```
http://<EC2_PUBLIC_IP>:3000
```

---

## Learning Outcomes

This project provided hands-on experience with:

* Infrastructure as Code (IaC)
* Terraform resource management
* AWS EC2, RDS, S3, VPC
* Automating application deployment
* Secure networking with security groups
* Real-world Node.js + MySQL architecture






## Author

**Dineth Sandakelum Herath**
Undergraduate | Cloud & DevOps Enthusiast
Sri Lanka




**


