# AWS LAMP Stack Project — WordPress with RDS MySQL

## 🚀 Project Overview
This project demonstrates how to deploy a **WordPress application** on an **EC2 instance (frontend)** with a **MySQL database hosted on Amazon RDS (backend)**, forming a **LAMP stack** architecture on AWS.

- **L**inux (Amazon Linux EC2)  
- **A**pache (Web Server)  
- **M**ySQL (Amazon RDS)  
- **P**HP (WordPress CMS)  

This setup separates the **frontend (WordPress)** and the **backend (MySQL DB)** to ensure scalability, reliability, and better management of resources.

---

## 🛠️ AWS Services Used
- **Amazon EC2** → Hosts WordPress (frontend)  
- **Amazon RDS (MySQL)** → Stores WordPress database (backend)  
- **Amazon VPC & Security Groups** → Networking & firewall rules  
- **IAM Role** → Secure instance access for SSM/permissions  

---

## 📑 Project Report
👉 [Click here to view/download the full PDF][[(https://drive.google.com/your-public-share-link)]](https://drive.google.com/file/d/1D2aWxYENuburDxGCn5jcYsyxSChBVlbs/view)

---

## 🔧 Deployment Steps (Summary)

### 1. Launch EC2 Instance (WordPress Frontend)
- AMI: Amazon Linux  
- Allowed inbound traffic on **Port 80 (HTTP)**  
- Installed required packages:
  ```bash
  sudo yum install -y httpd php mysql
  sudo service httpd start
````

### 2. Launch RDS (MySQL Backend)

* Engine: MySQL
* Created DB instance (e.g., `mysqlwp`)
* Allowed inbound traffic on **Port 3306** from WordPress EC2 security group.
* Saved the **RDS endpoint**.

### 3. Configure WordPress EC2

* Installed MySQL client:

  ```bash
  sudo yum install -y mysql
  ```
* Connected to RDS:

  ```bash
  mysql -h <RDS-ENDPOINT> -P 3306 -u admin -p
  ```
* Created DB & user:

  ```sql
  CREATE DATABASE wordpress;
  CREATE USER 'wpuser' IDENTIFIED BY 'root123456';
  GRANT ALL PRIVILEGES ON wordpress.* TO wpuser;
  FLUSH PRIVILEGES;
  ```

### 4. Install & Configure WordPress

* Download & extract WordPress:

  ```bash
  wget https://wordpress.org/latest.tar.gz
  tar -xzf latest.tar.gz
  cd wordpress
  ```
* Configure database settings in `wp-config.php`:

  ```php
  DB_NAME = wordpress
  DB_USER = wpuser
  DB_PASSWORD = root123456
  DB_HOST = <RDS-ENDPOINT>
  ```
* Move files to Apache web root:

  ```bash
  sudo cp -r * /var/www/html/
  sudo service httpd restart
  ```

### 5. Verify Setup

* Access `http://<EC2-Public-IP>`
* WordPress installation page appears → connected successfully to RDS DB.

---

## 📊 Real-Time Use Case

* Hosting blogs, news portals, and CMS platforms in the cloud.
* Decoupled architecture ensures **application (EC2)** and **database (RDS)** can scale independently.
* Used widely in production for **WordPress-based websites**.

---

## 📜 Key Commands Recap

```bash
# Install Apache, PHP, MySQL client
sudo yum install -y httpd php mysql

# Start Apache
sudo service httpd start

# Download & setup WordPress
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
cd wordpress
cp wp-config-sample.php wp-config.php
vi wp-config.php

# Move files & restart Apache
sudo cp -r * /var/www/html/
sudo service httpd restart
```

---

## ✅ Conclusion

This project validates a **working LAMP stack** on AWS using **EC2 + RDS**, showcasing how to host a **WordPress site** with a separate managed database.
The architecture is modular, secure, and production-ready.


