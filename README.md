# WordPress Deployment with Ansible and Docker

This project uses **Ansible** to automate the deployment of a full WordPress stack (MySQL, phpMyAdmin, WordPress) using Docker containers.

---

## 📌 Playbook Overview

The playbook `deploy_wordpress.yml` performs the following tasks:

1. **Create Docker Network**  
   Ensures a dedicated Docker network is created for container communication.

2. **Deploy MySQL Database**  
   Runs a MySQL container with configured root password, database, user, and persistent storage.

3. **Deploy phpMyAdmin**  
   Runs a phpMyAdmin container connected to the MySQL database.

4. **Deploy WordPress**  
   Runs a WordPress container connected to the MySQL database with persistent storage.

---

## 📂 Project Structure

```
project-root/
│── playbooks/
│   └── deploy_wordpress.yml
│── vars/
│   └── app.yml
│── README.md
```

---

## ⚙️ Variables (from `vars/app.yml`)

The following variables must be defined in `vars/app.yml`:

```yaml
# Database
db_name: db
db_image: mysql:latest
db_network: wordpress_network
db_ports:
  - "3306:3306"
db_root_password: root
db_database: wordpress
db_user: wpuser
db_password: wppass
db_volume: db_data:/var/lib/mysql

# phpMyAdmin
pma_name: phpmyadmin
pma_image: phpmyadmin:latest
pma_ports:
  - "8080:80"

# WordPress
wp_name: wordpress
wp_image: wordpress:latest
wp_ports:
  - "8081:80"
wp_volume: wp_data:/var/www/html
```

---

## ▶️ How to Run

1. Ensure Docker and Ansible are installed on the host machine.
2. Clone this repository and update the `vars/app.yml` file with your configuration.
3. Run the playbook:

```bash
ansible-playbook -i inventory.ini parameterized_playbook
```

---

## 🌍 Access Services

- **WordPress:** http://localhost:8081  
- **phpMyAdmin:** http://localhost:8080  

---

## 📖 Notes

- Ensure your firewall allows the exposed ports.
- Update variables in `vars/app.yml` as needed before running.
