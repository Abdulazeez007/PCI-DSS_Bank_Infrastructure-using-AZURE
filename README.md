
# PCI-DSS Compliant 3-Tier Bank Infrastructure on Azure

Welcome to my PCI-DSS compliant 3-tier banking project! This repository documents the setup of a secure, scalable, and compliant banking system using **Azure**, **Ubuntu**, **MySQL**, **Node.js**, and **Java**. It's designed to meet **PCI-DSS (Payment Card Industry Data Security Standards)**, ensuring secure handling of sensitive payment information.

---

## 🌟 **What Is This Project About?**

Imagine you're building a secure online banking platform that handles sensitive payment card data. This project demonstrates how to:

1. **Securely set up servers (frontend, backend, database)** on Azure.
2. Ensure the **highest level of security compliance** with PCI-DSS standards.
3. Use modern tools and best practices for monitoring, encryption, and access control.

---

## 🏗️ **How It Works**

This project uses a **3-tier architecture**:
- **Frontend**: A user-friendly web interface built with React.
- **Backend**: An API layer for handling business logic, secured with Java and Maven.
- **Database**: A secure MySQL database configured to meet PCI-DSS standards.

Each component is hosted on its own Azure virtual machine (VM), with carefully crafted rules for network security and access control.

---

## 🛠️ **Steps to Build This Infrastructure**

### 1. **Backend Server Setup**
- **Create the Server**:
  - Set up an Ubuntu server (`backend_vm`) on Azure.
  - Secure it with an SSH key for access.
- **Install Dependencies**:
  - Install Java Development Kit (JDK 17) and Maven for building and running the backend code.
  - Clone the backend code repository and configure it to connect to the database.
- **Test Connections**:
  - Use MySQL client to verify the backend can securely communicate with the database.

### 2. **Frontend Server Setup**
- **Create the Server**:
  - Set up another Ubuntu server (`frontend-G3-vm`) for the web interface.
- **Install Dependencies**:
  - Install Node.js (v14) and npm to run the frontend code.
  - Clone the frontend code repository and link it to the backend server.
- **Launch the Application**:
  - Start the frontend server, enable port 3000 for the browser, and test the interface.

### 3. **Database Setup (PCI-DSS Compliance)**
- **Secure the Database**:
  - Install MySQL, change default passwords, and enable encryption (for data at rest and in transit).
  - Configure logging and monitoring for all database activities.
- **Access Control**:
  - Create users with limited privileges using MySQL’s role-based access control (RBAC).
  - Use Azure Key Vault to securely store sensitive credentials.
- **Monitoring**:
  - Integrate with Azure Monitor and Log Analytics for real-time tracking of database activities.

---

## 🛡️ **What Makes It Secure?**

This project follows PCI-DSS v4.0 guidelines:
1. **Firewalls**: Network Security Groups (NSGs) restrict unauthorized access.
2. **Encryption**: Data is encrypted during storage and transmission.
3. **Access Controls**: Users only get the permissions they need.
4. **Monitoring**: Logs track every action, ensuring accountability.
5. **Regular Updates**: Servers and databases are patched for security.

---

## 🛠️ **Technologies Used**

- **Azure**: Hosting VMs and monitoring services.
- **Ubuntu**: Secure and reliable server OS.
- **MySQL**: PCI-DSS compliant database.
- **React**: Frontend development.
- **Java & Maven**: Backend development.
- **Node.js & npm**: Frontend dependency management.

---

## 📚 **Skills Demonstrated**

1. **Cloud Deployment**: Creating and securing Azure VMs.
2. **Network Security**: Using firewalls and secure access policies.
3. **Database Management**: Encryption, logging, and access control.
4. **Full-Stack Development**: Backend and frontend integration.
5. **Compliance Knowledge**: Implementing PCI-DSS standards.

---

## 🚀 **How to Run This Project**

## **Step 1: Backend Tier Setup**

### **Objective**: Deploy and configure the backend server with Java, Maven, and API access.

#### **1.1. Create the Backend Server**
1. Go to the **Azure Portal**.
2. Navigate to **Virtual Machines** and click **Create** > **Virtual Machine**.
3. Fill in the details:
   - **Name**: `backend_vm`
   - **Region**: Choose your nearest Azure region.
   - **Image**: Ubuntu Server 22.04 LTS.
   - **Size**: Standard DS1_v2 (1vCPU, 3.5GB RAM).
4. Under **Administrator Account**, choose SSH public key and paste your key (use `ssh-keygen -b 4096` to generate one if you don’t have it).
5. Under **Networking**, associate the **Network Security Group (NSG)** created in the next step.

---

#### **1.2. Configure Network Security Group (NSG)**
1. Go to the **NSG** associated with the backend VM.
2. Add inbound rules:
   - **Allow SSH (port 22)** from your IP.
   - **Allow HTTP (port 4000)** from the frontend IP **172.20.0.0**.
   - Deny all other traffic by default.

---

#### **1.3. Install Java and Maven**
1. Connect to the backend VM using an SSH client:
   ```bash
   ssh -i <private_key> azureuser@<backend_vm_public_ip>
   ```
2. Update and upgrade the system:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```
3. Install Java 17:
   ```bash
   sudo apt install openjdk-17-jdk openjdk-17-jre -y
   ```
4. Install Maven:
   ```bash
   sudo apt install maven -y
   ```

---

#### **1.4. Deploy Backend Code**
1. Install Git:
   ```bash
   sudo apt install git -y
   ```
2. Clone your backend repository:
   ```bash
   git clone https://username:gittoken@remote-repo-link
   ```
3. Navigate to the repository folder:
   ```bash
   cd <repository_folder>
   ```
4. Update database credentials in the `application.properties` file:
   ```properties
   spring.datasource.url=jdbc:mysql://172.20.1.4:3306/online_banking_system
   spring.datasource.username=<db_user>
   spring.datasource.password=<db_password>
   ```

---

#### **1.5. Test Database Connection**
1. Install MySQL client:
   ```bash
   sudo apt install mysql-client -y
   ```
2. Test the connection:
   ```bash
   mysql -u <db_user> -p<db_password> -h 172.20.1.4
   ```

---

## **Step 2: Frontend Tier Setup**

### **Objective**: Deploy and configure the frontend server with React and Node.js.

#### **2.1. Create the Frontend Server**
1. In **Azure Portal**, navigate to **Virtual Machines** and create a new VM.
2. Fill in the details:
   - **Name**: `frontend-G3-vm`
   - **Region**: Same as the backend server.
   - **Image**: Ubuntu Server 22.04 LTS.
   - **Size**: Standard DS1_v2.
3. Secure with an SSH key, as done for the backend server.

---

#### **2.2. Configure Network Security Group (NSG)**
1. Go to the **NSG** associated with the frontend VM.
2. Add inbound rules:
   - **Allow SSH (port 22)** from your IP.
   - **Allow HTTP (port 3000)** for web traffic.
   - **Allow HTTPS (port 443)** for secure connections.

---

#### **2.3. Install Node.js and npm**
1. SSH into the frontend VM:
   ```bash
   ssh -i <private_key> frontendadmin@<frontend_vm_public_ip>
   ```
2. Update the system:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```
3. Install Node.js (version 14):
   ```bash
   curl -fsSL https://deb.nodesource.com/setup_14.x | sudo -E bash -
   sudo apt install -y nodejs
   ```

---

#### **2.4. Deploy Frontend Code**
1. Clone your frontend repository:
   ```bash
   git clone https://username:gittoken@remote-repo-link
   ```
2. Update the frontend code to use the **backend private IP (172.20.0.0)**:
   - Open the source files in the `src/` folder using:
     ```bash
     nano <file_name>
     ```
   - Replace any occurrences of `localhost` with `172.20.0.0`.
3. Start the application:
   ```bash
   npm install
   npm start
   ```

---

## **Step 3: Database Tier Setup**

### **Objective**: Deploy a secure MySQL database that meets PCI-DSS compliance.

#### **3.1. Create the Database Server**
1. Create a new VM in Azure:
   - **Name**: `mysql-server`.
   - **Region**: Same as the other servers.
   - **Image**: Ubuntu Server 22.04 LTS.
   - **Size**: Standard DS1_v2.
2. Secure the VM with an SSH key.

---

#### **3.2. Secure the Database**
1. SSH into the VM:
   ```bash
   ssh -i <private_key> azureuser@<database_public_ip>
   ```
2. Install MySQL:
   ```bash
   sudo apt install mysql-server -y
   ```
3. Secure the MySQL installation:
   ```bash
   sudo mysql_secure_installation
   ```
4. Edit the MySQL configuration file to bind to the VM’s private IP:
   ```bash
   sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
   ```
   Update:
   ```ini
   bind-address = 172.20.1.4
   ```

---

#### **3.3. Implement Compliance**
1. Enable encryption:
   - For data at rest: Use MySQL’s `InnoDB` encryption.
   - For data in transit: Configure SSL/TLS.
2. Create users with specific privileges:
   ```sql
   CREATE USER 'app_user'@'%' IDENTIFIED BY 'SecurePassword123!';
   GRANT SELECT, INSERT, UPDATE, DELETE ON online_banking.* TO 'app_user'@'%';
   ```
3. Enable logging:
   ```ini
   general_log = 1
   general_log_file = /var/log/mysql/mysql.log
   ```

---

## 📢 **Why This Project Stands Out**

This isn't just a demo; it’s a blueprint for real-world banking systems. The project showcases:
- A comprehensive understanding of **security-first development**.
- The ability to configure and integrate tools across multiple environments.
- A clear commitment to **industry standards**.

---

Here’s the finalized version with a **detailed summary**, **conclusion**, and **recommendations** added to make the documentation comprehensive and insightful for prospective reviewers.

---

## **Summary**

This project demonstrates the design and deployment of a **3-tier bank infrastructure** that complies with **PCI-DSS v4.0 standards**, ensuring the secure handling of sensitive payment data. Using **Azure** as the hosting platform, the project implements a layered approach to secure operations:

- **Frontend Tier**: Hosts the user interface built with React, running on an Ubuntu VM.
- **Backend Tier**: Contains business logic and API services written in Java, hosted on a separate Ubuntu VM.
- **Database Tier**: Secures payment-related data in a MySQL database configured for PCI-DSS compliance.

By leveraging industry best practices such as encryption, access control, and real-time monitoring, this project effectively showcases end-to-end security and regulatory compliance for banking systems.

### **Key Features**
1. **Azure Integration**:
   - Virtual Machines for isolated tiers.
   - Network Security Groups (NSGs) to manage traffic.
   - Azure Monitor and Log Analytics for real-time monitoring.
2. **Security Measures**:
   - Encrypted data storage and communication (SSL/TLS).
   - Role-based access control for database users.
   - Comprehensive logging for auditing and tracking.
3. **Compliance Adherence**:
   - Maps PCI-DSS requirements (e.g., encryption, logging, user authentication) to specific implementation steps in Azure.
4. **Scalability**:
   - Architecture supports scaling individual tiers independently.

---

## **Conclusion**

The deployment of this infrastructure highlights the importance of a structured and secure approach to designing financial systems. By breaking the solution into three distinct tiers, this architecture ensures:

- **Data Security**: Separation of concerns reduces the risk of data leakage or unauthorized access.
- **Regulatory Compliance**: Implementation aligns with PCI-DSS v4.0 standards, meeting critical industry requirements.
- **Reliability**: Each component is designed to operate independently, ensuring system uptime and resilience.

The use of **Azure's powerful tools**, such as NSGs, Key Vault, and Log Analytics, further strengthens the system's security posture while simplifying management and monitoring.

This project serves as a **practical guide for implementing PCI-DSS compliant systems** in real-world scenarios, providing a secure and scalable solution for organizations handling sensitive payment information.

---

## **Recommendations**

To enhance and further optimize the infrastructure, the following recommendations are proposed:

1. **Automation**:
   - Use **Infrastructure as Code (IaC)** tools like Terraform or Azure Resource Manager (ARM) templates to automate VM creation, NSG configuration, and resource provisioning.
   - Automate regular updates and security patches using tools like Ansible or Azure Update Management.

2. **Advanced Monitoring**:
   - Leverage **Azure Sentinel** for centralized security management and advanced threat detection.
   - Set up alerts for unusual activities, such as unauthorized database access attempts or excessive API calls.

3. **Performance Optimization**:
   - Implement **load balancing** for the frontend and backend tiers to handle high traffic efficiently.
   - Use **Azure Database for MySQL** as a managed solution to offload maintenance tasks such as backups and performance tuning.

4. **Enhanced User Access Controls**:
   - Integrate **Azure Active Directory (Azure AD)** for seamless user management and Multi-Factor Authentication (MFA).
   - Limit SSH access to VMs using Just-In-Time (JIT) access in **Azure Security Center**.

5. **Periodic Security Audits**:
   - Conduct regular vulnerability scans and penetration testing to ensure no new security gaps emerge.
   - Review compliance against the latest PCI-DSS standards to adapt to evolving requirements.

6. **Documentation**:
   - Maintain up-to-date internal documentation for each tier, including configuration changes, new user roles, and updated IP rules.
   - Provide training for the team to ensure smooth handover and operational continuity.

