  
	web-servers-playbook.yaml

	https://docs.ansible.com/ansible/latest/user_guide/playbooks.html

	https://docs.ansible.com/ansible/latest/collections/ansible/builtin/package_module.html

	---
	 - hosts: 
	   become: 
	   tasks:
	   - name: 
	     yum:
	      name: 
	      state:

	---
	 - hosts: webservers
	   become: yes
	   tasks: 
	   # Task 1 "Installing Apache"
	   - name: Installing apache in production
	     yum: 
	      name: 
	      state:
	   # Task 2 "Starting Apache"
	   - name:
	     module:
	      name: 
	      state:

From  Ibiba briggs  to  Everyone:
	https://docs.ansible.com/ansible/latest/user_guide/intro_adhoc.html#managing-services

	---
	 - hosts: appservers
	   become: yes
	   tasks: 
	   # Task 1 "Installing apache tomcat in production"
	   - name: Installing apache tomcat software
	     yum: 
	      name: tomcat
	      state: latest
	   # Task 2 "Starting apache tomcat"
	   - name: Starting apache tomcat
	     service:
	      name: tomcat
	      state: started


sudo hostname webserver =============================> To change the host name of the master server to webserver. The Master server though being the ochestrator, will also act as one of the servers taking part in the workload.

sudo hostname appserver =============================> To change the host name of the client1 server to appserver

sudo hostname dbserver ==============================> To change the host name of the client2 server to dbserver

sudo vi /etc/ansible/hosts ==========================> To to update the Inventory file of the Master with the ip addresses and group/domain names

ansible <group> -m ping =============================> To test connection between the ochestrator and the different host/group servers

ansible webservers -m ping ==========================> To test connection between the host and the webservers (Error was reported because the RSA key was not shared with the master since the master was only initially meant to be an ochestrator, and not to take part in the workload)

ansible appservers -m ping ==========================> To test connection between the host and the appservers

ansible dbservers -m ping ==========================> To test connection between the host and the dbservers

ssh-copy-id ansible@Internal/PrivateIP =============> To copy RSA key from the Master to any client server

ssh-copy-id ansible@10.128.0.2 =====================> To copy RSA key from the Master to any master-webserver

ansible webservers -m ping ==========================> To test connection between the host and the webservers = Successful

vi web-servers-playbook.yaml ========================> To create and edit the file at the same time

allUsers ============================================> Using the allUsers function to make the bucket public when Mathew could not sync his files with the Master server due to permissions issues

gsutil rsync gs://bucketname .  =====================> To Sync your gcs bucket data with your local

gsutil rsync gs://test_bucket_bucket_001 . ==========> Actual command after editing. The last (.) in the command actually specifies the current location you are copying the files to.

ansible-playbook playbook-name --syntax-check =======> To check the Playbook syntax before execution

ansible-playbook web-servers-playbook.yaml --syntax-check ==> To check the webserver Playbook syntax before execution
ansible-playbook app-servers-playbook.yaml --syntax-check ==> To check the appserver Playbook syntax before execution
ansible-playbook db-servers-playbook.yaml --syntax-check  ==> To check the dbserver Playbook syntax before execution

ansible-playbook playbook-name --check =====================> A dry-run to see the changes that will be done in the environment...just like running "terraform plan"

ansible-playbook web-servers-playbook.yaml --check =========> A dry-run to see the changes that will be done in the webserver environment

ansible-playbook app-servers-playbook.yaml --check =========> A dry-run to see the changes that will be done in the appserver environment

ansible-playbook db-servers-playbook.yaml --check ==========> A dry-run to see the changes that will be done in the dbserver environment

sudo systemctl status httpd ================================> To check the status of apache. If it was installed, you will see that. If it was a dry-run, no changes will be made.

ansible-playbook web-servers-playbook.yaml --check -v ==========> A dry-run with verbosity. The more v that you have, the more verbosity output that you will see

ansible-playbook web-servers-playbook.yaml --check -vvvvvv ==========> A dry-run with verbosity. The more v that you have, the more verbosity output that you will see

ansible-playbook web-servers-playbook.yaml ==========================> Actual execution of the webserver ansible playbook. 2 changes made. Apache installed and started. 

sudo systemctl status httpd ================================> To check the status of apache after installation and strting apache

ansible-playbook app-servers-playbook.yaml =================> To execute the appserver playbook

ansible-playbook app-servers-playbook.yaml -vv =============> To execute the appserver playbook but running verbosity to track the execution process...in case there is a problem along the way - you can capture it instantly.

sudo systemctl status tomcat ===============================> To chect the status of apache tomcat

ansible-playbook db-servers-playbook.yaml ==================> To execute the dbserver playbook