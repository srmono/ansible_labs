GCP -> Goole Cloud
Project ID: venkata-practice 
Service Account: create and download the key
    
1. Controller machine
    Ubuntu/Redhat/CentOS
    Cloud Console

    - install google-auth
        sudo pip install intall google-auth

2. Create a dedicated inventory directory

   sudo mkdir -p /opt/ansible/inventory

3. Change permissions to directory

    sudo chmod -R 755 /opt/ansible/

4. create separate Service Account for ansible
[owner/oslogin]
    service-account.json

5. update default inventory inside ansible.cfg

sudo vi /etc/ansible/ansible.cfg

[defaults]
inventory = /opt/ansible/inventory/gcp.yml

6. Create gcp.yml and service-account.json

cd /opt/ansible/inventory
sudo vi service-account.json

note: copy and paste the key which you have downloaded in previous steps

-- Create gcp.yml file

sudo vi gcp.yml

--- 
plugin: gcp_compute
projects: 
  - venkata-practice
auth_kind: serviceaccount
service_account_file: service-account.json
keyed_groups:
  - key: labels
    prefix: label 
  - key: zone 
    prefix: zone 
groups: 
  remote: "'java' in (lables|list)"


7. Check list of inventory avaialble

ansible-inventory --list -i gcp.yml

ansible-inventory -i gcp.yml --graph


