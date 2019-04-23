# README #

### Installation ###

# 		Pre-Installation:
Install ansible :

`sudo pip install ansible`

Clone the project :

`git clone https://github.com/fufulift/Tp-Ansible-Ops.git`

# 		Launching
Use this command :

`ansible-playbook playbook/playbook.yml -i ./inventory.ini`

# 		Be careful to :
Edit remote_user in "ansible.cfg"
Add path to private key file

```
[default]
remote_user = [username]
private_key_file = [path_ssh_key]
inventory = ./inventory.ini
host_key_checking = False
```

Go to "host_vars/" and edit file name to virtual env name
Add virtual env's ip

```
ansible_host: [ip_address]
```

Edit remote_user in "playbook/playbook.yml"

```
- hosts: web
  remote_user: [username]
  become: true
  gather_facts: False
  tasks:
```

Edit params in "playbook/mysql/defaults/main.yml"

```
mysql_user_home: [home]
mysql_user_name: [name]
mysql_user_password: [password]
wp_db_name: [db_name]
```

Edit host in "paybook/mysql/tasks"

```
- name: Create wordpress user
  become: true
  become_user: root
  mysql_user:
    name: wordpress
    host: [private_ip]
    password: P@ssw0rd
    priv: '*.*:ALL,GRANT'
    state: present
```

Edit params in "playbook/wordpress/defaults/main.yml"

```
mysql_user_name: [user]
mysql_user_password: [password]
wp_db_name: [db_name]
wp_db_host: [private_ip]
```