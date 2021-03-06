# Auth Key Portal
A self service portal for storing ssh authorized_keys in a custom LDAP attribute.

### Background

I was architecting and standing up some infrastructure in AWS for a client who required key based login for their EC2 nodes without using a solution like EFS. Thus I wrote this simple portal code.

### Setup
#### Step 1 - Install Dependencies

```sh
sudo apt install nginx php7.0-fpm php7.0-ldap ldb-tools samba
```
#### Step 2 - Configure NGINX
#### Step 3 - Modify LDAP Schema

```
ldbmodify -H "ldap://domain.local" modification.ldif --user "<Admin Account>" --password "<Admin Password>"
```

#### Step 4 - Clone repo into desired folder

#### Step 5 - Update config.php

### Configuring Nodes

1. sudo cp auth-key-command.sh /opt/auth-key-command.sh
2. Update HOST variable with the server that runs the php code in auth-key-command.sh
3. Make file executeable (sudo chmod +x /opt/auth-key-command.sh)
4. Add the following to the end of /etc/ssh/sshd_config

  ```
  AuthorizedKeysCommand /opt/auth-key-command.sh
  AuthorizedKeysCommandUser nobody
  ```
5. Restart ssh service

  ```
  sudo service ssh restart
  ```

**Optional**
- Add line to end of  /etc/pam.d/ssh

```
session    required   pam_mkhomedir.so skel=/etc/skel/ umask=0022
```

### Screenshots

#### Login Page
![Login](/screenshot-1.png)

#### Dashboard Page
![Dashboard](/screenshot-2.png)

#### Add Key Dialog
![Add Key Dialog](/screenshot-3.png)
