## ANSIBLE AD-HOC COMMANDS
### Copying Files Using The "Copy Module" In Ansible 
```
touch application.txt
ansible webservers -m copy -a "src=/home/ansible/application.txt dest=/home/ansible"
```
```
touch java-app.jar
ansible webservers -m copy -a "src=/home/ansible/java-app.jar dest=/home/ansible"
```

### Creating users using the "User Module" In Ansible 
```
ansible all -m user -b -a "name=Joshua password=|password_hash[Joshua]"
```

### Changing File Permissions Using "File Module" In Ansible
```
ansible webservers -b -m file -a "dest=/home/ansible/java-app.jar mode=777 owner=Joshua"
```

### Deleting Files Using "File Module" In Ansible => absent
```
ansible webservers -b -m file -a "dest=/home/ansible/application.txt state=absent"
```  

### Installing Softwares Using The "Yum Module" In Ansible => Ansible also supports the Yum Command
### We will install Apache across all the servers 
```
ansible webservers -b -m yum -a "name=httpd state=present"
```

### Managing Services In Linux Using The "Service Module" In Ansible
### sudo systemctl status httpd => To Chaeck the status of apache - whether live (running) or dead (not running)
```
ansible webservers -b -m service -a "name=httpd state=started"
```