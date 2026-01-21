# Installing Frappe Framework and ERPNext on Ubuntu. 
Open the terminal.

Step-1: Upgrade the system:
Bash command: sudo apt update && sudo apt upgrade -y

Step-2: Install Required Dependencies:
sudo apt install -y \
git curl sudo \
python3 python3-pip python3.12-venv \
redis-server mariadb-server mariadb-client \
nodejs npm \
wkhtmltopdf \
software-properties-common

Step-3: Install Node.js (recommended for v15):
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs

Step-4: Install Yarn:
sudo npm install -g yarn

Step-5: Install Bench CLI:
sudo pip3 install frappe-bench
-> To verify: 
bench --version

Step-6: Start & enable MariaDB:
sudo systemctl start mariadb
sudo systemctl enable mariadb

Step-7: Configure MariaDB
sudo mysql_secure_installation
-> Then:
sudo mysql
-> We will see below questions. Prper answer to them are given below:
Switch to unix_socket authentication? → n
Set root password? → y
Enter new password → (your password)
Remove anonymous users? → y
Disallow root login remotely? → y
Remove test database? → y
Reload privilege tables? → y
-> If you want to change the root password then do this:
Change the root password? → Y
New password: password
Re-enter new password:password 
/* Enter a strong password — remember this password, because Frappe will ask for it when creating the site.*/

Step-8: Install Node.js (LTS) & Yarn
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs
sudo npm install -g yarn
-> To verify: 
node -v
yarn -v

Step-9: Install pipx (required for Ubuntu 24.04):
sudo apt install -y pipx
pipx ensurepath

Step-10: Install Bench:
pipx install frappe-bench
-> To verify:
which bench
bench --version

Step-11: Initialize Frappe Bench (THIS installs Frappe):
bench init frappe-bench --frappe-branch version-15

Step-12: Enter bench folder:
cd frappe-bench

Step-13: Create a new site: 
bench new-site mysite.local

Step-13: Install ERPNext: 
bench get-app erpnext --branch version-15
bench --site mysite.local install-app erpnext

Step-14: Set default site
bench use mysite.local

Step-15: Start the server:
bench start

Step-16: Open Browser:
http://localhost:8000

Login:
Username: Administrator
Password: (the one we set)

-> How to verify everything: 

bench version
bench --site mysite.local list-apps
ls
cd ~/frappe-bench
ls sites
mysql --version
redis-server --version
node -v
python3 --version
