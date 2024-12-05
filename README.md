# Ansible Playbooks
These are ansible scripts I've used to add [Wazuh](https://wazuh.com/), [Sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon), and additional logging on [GOAD lab (with ludus behind the scenes)](https://docs.ludus.cloud/docs/environment-guides/goad).
# Example
First you need your inventory file. If you've followed along with Ludus + GOAD install, you already have one in GOAD/ansible folder. 
```
~/ansible$ cat inventory-goad-light.yml 
[default]
; ------------------------------------------------
; sevenkingdoms.local
; ------------------------------------------------
dc01 ansible_host=10.3.10.10 dns_domain=dc01 dict_key=dc01
; ------------------------------------------------
; north.sevenkingdoms.local
; ------------------------------------------------
dc02 ansible_host=10.3.10.11 dns_domain=dc01 dict_key=dc02
srv02 ansible_host=10.3.10.22 dns_domain=dc02 dict_key=srv02

[all:vars]
force_dns_server=no
dns_server=10.3.10.254

dns_server_forwarder=10.3.10.254

; winrm connection (windows)
ansible_user=localuser
ansible_password=password
ansible_connection=winrm
ansible_winrm_server_cert_validation=ignore
ansible_winrm_operation_timeout_sec=400
ansible_winrm_read_timeout_sec=500
```
Then use one of the playbooks like so:
`ansible-playbook -i inventory-goad-light.yml ad-operations-audit.yaml`

# Useful Links
https://wazuh.com/blog/hunting-for-windows-credential-access-attacks/
https://wazuh.com/blog/how-to-detect-active-directory-attacks-with-wazuh-part-1-of-2/
https://wazuh.com/blog/how-to-detect-active-directory-attacks-with-wazuh-part-2/
