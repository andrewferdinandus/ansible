📦 Ansible Playbook: Deploy MySQL Database Server on AWS EC2
This Ansible playbook automates the installation and configuration of a MySQL database server on a Linux EC2 instance running Ubuntu/Debian in AWS.

📋 Features
Installs mysql-server package

Sets root password securely

Configures MySQL to allow remote connections

Enables and starts the MySQL service

Opens the MySQL port (3306) on the firewall

Uses handlers to restart MySQL if the config changes

🧰 Prerequisites
AWS EC2 instance running Ubuntu/Debian

SSH access via private key (.pem)

Ansible installed on your control machine

Python bindings (python3-mysqldb) installed on the target host

Ansible Collections:

ansible-galaxy collection install community.mysql
📁 Project Structure
bash
Copy
Edit
.
├── deploy_mysql_db.yaml       # Main Ansible playbook
├── hosts.ini                  # Inventory file
└── README.md                  # This documentation

🛠️ Configuration
hosts.ini
Define your EC2 instance in the inventory file:

[dbservers]
**<instance_ip>** ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/your-key.pem
Replace the IP, username, and key path as needed.

🚀 Running the Playbook
To execute the playbook:

ansible-playbook -i hosts.ini deploy_mysql_db.yaml

🔐 Security Notes
Replace the hardcoded root password with a secure method in production (e.g., Ansible Vault or environment variables).

Remote root login is enabled for demonstration. Disable it in production.

Ensure AWS Security Groups allow inbound TCP traffic on port 3306 if remote access is needed.

🧼 Cleanup
To remove MySQL:
ansible -i hosts.ini -m apt -a "name=mysql-server state=absent" dbservers -b
