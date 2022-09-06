Refer the repo of the role
https://github.com/srmono/ansible_role

1. Initiate role with galaxy

ansible-galaxy init /etc/ansible/roles/apache --offline 

2. cd to apache directory
 tree apache/

3. split the tasks into tasks directory
importing into main.yml file 
    - import_tasks: install.yml
    - import_tasks: config.yml
    - import_tasks: service.yml

4. cd handlers
    update restart task in main.yml
- name: Restart Apache Service
      service:
        name: httpd
        state: restarted 

5. cd meta
    update meta data for galaxy

6. create setup.yml file inside ansible directory
    cd /etc/ansible
    sudo vi setup.yml
[root@ansible ansible]# cat setup.yml 

---
- name: 
- hosts: all
  roles:
    - apache

7. run the file as a root user as we need to install apache

    sudo -i

    ansible-playbook setup.yml


-------------------------------------------

Upload on role on ansible galaxy

*- List roles

ansible-galaxy list

*- check git version on controller 

    git --version

*- install git

dnf install -y git 

*- Create apache.yml file inside apache role directory
/etc/ansible/roles/apache

[root@ansible apache]# cat apache.yml 
---
- name: Apache Server Configuration
- hosts: all
  roles:
    - apache

[root@ansible apache]# ls
apache.yml  defaults  files  handlers  meta  README.md  tasks  templates  tests  vars

*- Initiate git repo inside apache dir
[root@ansible apache]# git init

git add .
git commit -m "message"
git remote add origin https://github.com/srmono/ansible_role.git

*- Git configuration

git config user.name srmono
git config user.email bvsrao91@gmail.com

*- Push role to github repo
git push origin master

*- Create account on ansible-galaxy
https://galaxy.ansible.com/login?error=false&next=%2Fsrmono%2Fansible_role

*- From mycontent tab

click on add content
select upload from git
select the repo
and update

*- galaxy commands

ansible-galaxy search role_name
ansible-galaxy search user_name

ansible-galaxy info role_name

*- Install role

ansible-galaxy install srmono.ansible_role




