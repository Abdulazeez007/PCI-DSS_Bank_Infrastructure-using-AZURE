
# Backend Server Setup

This guide details the steps to configure the backend server as part of the PCI-DSS compliant 3-tier bank infrastructure.

## Tasks

### 1. Allow Access to Port 3306 in the Database Server
- Go to Network Security Group (NSG).
- Create a rule to allow the backend server to access the database on port 3306.

### 2. Create Backend Server
- Launch an Ubuntu VM named `backend_vm` on Azure.
- Secure the server with an SSH key:
  ```bash
  ssh-keygen -b 4096
  ```

### 3. Install JDK 17 & Maven
- Log in to the server and run:
  ```bash
  sudo apt update && sudo apt upgrade -y
  sudo apt install openjdk-17-jdk openjdk-17-jre -y
  sudo apt install maven -y
  ```

### 4. Pull Code into the Server
- Install Git if not present:
  ```bash
  sudo apt install git -y
  ```
- Clone the repository and update database credentials in `application.properties`.

### 5. Test Database Connection
- Install MySQL client:
  ```bash
  sudo apt install mysql-client -y
  ```
- Test connection using private IP after updating NSG rules.

### 6. Package Code with Maven
- Navigate to the project folder and package the code:
  ```bash
  mvn clean package
  ```

