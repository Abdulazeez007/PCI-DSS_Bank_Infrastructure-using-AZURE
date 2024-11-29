
# Frontend Server Setup

This guide covers the setup of the frontend server for the PCI-DSS compliant infrastructure.

## Tasks

### 1. Create Frontend Server
- Launch an Ubuntu VM named `frontend-G3-vm`.
- Secure the server with an SSH key.

### 2. Install Dependencies
- Update the server and install Node.js and npm:
  ```bash
  sudo apt update && sudo apt upgrade -y
  curl -fsSL https://deb.nodesource.com/setup_14.x | sudo -E bash -
  sudo apt install -y nodejs
  ```

### 3. Pull Code into the Server
- Clone the frontend repository and configure it to use the backend server's private IP.

### 4. Test Connection
- Install React dependencies:
  ```bash
  npm install
  npm start
  ```
- Enable frontend NSG rules for ports 3000 and 443.

