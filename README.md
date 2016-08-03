#LDAP

### Background

I was architecting and standing up some infrastructure in AWS for a client who required key based login for to the EC2 nodes without using a solution like EFS. Thus I wrote this simple portal code.

### Info

This portal uses LDAP for authentication.

### Setup
#### Step 1 - Install Dependencies

```sh
sudo apt install nginx php7.0-fpm php7.0-mysql mysql-server php7.0-ldap
```
#### Step 2 - Configure NGINX
#### Step 3 - Create database ensure privileges

```sql
CREATE SCHEMA ssh_config;
GRANT ALL PRIVILEGES ON ssh_config.* TO '<user>'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

#### Step 4 - Clone repo into desired folder

#### Step 5 - Update config.php

#### Configuring Nodes

1. sudo cp auth-key-command.sh /opt/auth-key-command.sh
2. Make file executeable (sudo chmod +x /opt/auth-key-command.sh)
3. Add the following to the end of /etc/ssh/sshd_config
```
AuthorizedKeysCommand /opt/auth-key-command.sh
AuthorizedKeysCommandUser root
```


**Optional**
- Add line to end of  /etc/pam.d/ssh

```
session    required   pam_mkhomedir.so skel=/etc/skel/ umask=0022
```

4. Restart ssh service
```
sudo service ssh restart
```