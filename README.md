# ansible

```
## Ansible labs

This repository contains my Ansible experiments and playbooks.  
The first project automates the *installation and configuration of Nginx* web server on multiple AWS EC2 instances using Ansible from a control node.  

---

## Environment 
- *Control Node:* Ubuntu VM (running Ansible)  
- *Managed Nodes:* 2 × AWS EC2 instances (Ubuntu)  
- *Connectivity:* Ansible communicates via SSH using inventory file  

## Example inventory
[webservers]
webserver1 ansible_host=ec2-public-dns-1 ansible_user=ubuntu
webserver2 ansible_host=ec2-public-dns-2 ansible_user=ubuntu
```
```bash
##Run this playbook against inventory
ansible-playbook -i inventory.ini nginx.yml
```
```
##Playbook execution outcome
PLAY [Install & Start Nginx] ***************************************************

TASK [Gathering Facts] *********************************************************
ok: [myec2.1]
ok: [myec2.2]

TASK [Install nginx] ***********************************************************
changed: [myec2.2]
changed: [myec2.1]

TASK [Start & enable nginx] ****************************************************
ok: [myec2.2]
ok: [myec2.1]

PLAY RECAP *********************************************************************
myec2.1                    : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
myec2.2                    : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```
```## EC2 instance outcome
sudo systemctl status nginx
systemctl status nginx
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: en>
     Active: active (running) since Fri 2025-09-19 10:22:13 UTC; 5min ago
     Main PID: 6634 (nginx)
      Tasks: 3 (limit: 1017)
     Memory: 2.4M (peak: 5.3M)
```

