# Setting up a LAMP server on my local Ubuntu VM

### 1. Prepare Ubuntu Server (Update and Upgrade)
- Updates have to be run as sudo, so `sudo apt update` and `sudo apt upgrade`.
- I created and saved an alias in my .bashrc file, so the word **update** runs both commands for me, when i type it in.

### 2. Install Apache
- Apache is a webserver. A webserver is a node that "serves" webpages when ypu request for them.
- Install Apache with `sudo apt install apache2`.
- Apache generally comes enabled by default. So once it is installed, it starts running.
- To check for the status of Apache, run: `systemctl status apache2`.
- If it isn't running, start the service with: `systemctl start apache2`.

### 3. Check if firewall is installed, enabled and if it allows web traffic
- To check if firewall (ufw) is installed: `ufw --version`.
- <img width="442" alt="UFW_version" src="https://user-images.githubusercontent.com/69907708/205644821-ac445e17-0ff2-48e8-a111-e4aaa9e2bfcb.png">
- If it isn't, run `sudo apt install ufw`.
- To check if it is enabled: `sudo systemctl status ufw`.
- If it isn't running, run `sudo systemctl start ufw`.
- To check if it has a profile for Apache, run `sudo ufw app list`.
- <img width="405" alt="UFW_list" src="https://user-images.githubusercontent.com/69907708/205644943-b1921920-d493-4e92-bc45-b4c809c51552.png">
- Run `sudo ufw app info "Apache Full"` to see if it enables traffic to ports **80** and **443**.
- <img width="705" alt="UFW_apache" src="https://user-images.githubusercontent.com/69907708/205645060-edea3543-88a1-4eec-aed0-235349e1f791.png">
- If it doesn't allow traffic to the ports, run `sudo ufw allow "Apache Full"`.

### 4. Install a Database (MariaDB)
- Install the required packages for MariaDB using: `sudo apt install mariadb-server mariadb-client`.
- Once installation is done, check to se if it is running properly using: `sudo systemctl status mariadb`.
- Secure the newly installed MariaDB service using: `sudo mysql_secure_installation`.

### 5. Install PHP and other dependencies
- Install the latest version of PHP using: `apt install php-common libapache2-mod-php php-cli php-mysql php-curl`.

### 6. Create a test page and edit apache conf file
- I will be using the phpinfo page as my test page.
- Create a file (info.php) in the web root directory using: `sudo nano /var/www/html/info.php`.
- Insert the PHP code below into the file:
`<?php
phpinfo ();
?>`
- Save and close the file.
- Modify the way apache serves files by editing the dir.conf file so that index.php is the first file: `sudo nano /etc/apache2/mods-enabled/dir.conf`.

### 7. Restart Apache
- Restart apache service using: `sudo systemctl restart apache2`.

### 8. Open Test Page
- Open the test page in your browser by visiting: `localhost/info.php`.
- <img width="1368" alt="testpage" src="https://user-images.githubusercontent.com/69907708/205645586-ec7fd0bc-b927-4bed-acc2-1f0ebb556cc3.png">

