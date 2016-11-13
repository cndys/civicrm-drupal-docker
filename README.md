
# Aim

To have a basic CiviCRM with drupal working website.

For tests purpose, not (at all) production ready!

# Installation

1. git clone https://github.com/cndys/civicrm-drupal-docker
2. docker-compose build
3. docker-compose up &

If you want to see your running containers: docker ps
If you need to enter in a container: docker exec -it [container name/id] bash

You can go to localhost (Linux) or 192.168.99.100 (Mac or Windows, it's actually your VM's ip).

4. Go to phpMyAdmin : localhost:8080 or 192.168.99.100:8080
Create 2 db: drupal-civi and civicrm

5. Go to Drupal and install it: localhost or 192.168.99.100
For database settings:
 - ip : 192.168.99.100
 - port: 3306
 - login: root
 - password: password (security firts... so, you understand the "not (at all) prod ready...")

6. If you accessed to the Drupal homepage, you can go to the CiviCRM's module install page: <localhost or 192.168.99.100>/sites/all/modules/civicrm/install/index.php 
7. Fill the information for the 2 databases: civicrm (CiviCRM) and Drupal (drupal-civi) with "root" and "password" on "localhost" or 192.168.99.100

If you did not manage to install CiviCRM with Drupal on Docker post your issues here! 
