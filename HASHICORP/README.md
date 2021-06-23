# HashiCorp Vault 연동

## OTP playbook
```yaml
---
- name: Get OTP Info
  hosts: vault
  gather_facts: false 
  
  tasks: 
  - name: Get OTP From HashiCorp Vault
    uri: 
      url: {{ HASHICORP_VAULT_URL }}/v1/ssh/creds/otp_key_role
      method: POST 
      headers:
        Content-Type: application/json
        X-Vault-Token: "{{ X_VAULT_TOKEN }}"
      body_format: json
      body:  {"ip" : "{{ inventory_hostname }}"}
      return_content: yes
    register: otp
    delegate_to: 127.0.0.1

  - name: Print All variables of data in HashiCorp Vault 
    debug:
      msg: "{{ otp }}" 
    delegate_to: 127.0.0.1

  - name: Print username,key of data in HashiCorp Vault 
    debug:
      msg: "username : {{ otp.json.data.username }}, key : {{ otp.json.data.key }}" 
    delegate_to: 127.0.0.1

  - name: Setting host facts(username,key) using data in HashiCorp Vault 
    set_fact:
      ansible_user: "{{ otp.json.data.username }}"
      ansible_password: "{{ otp.json.data.key }}"
    delegate_to: 127.0.0.1

  - name: Print secret information using data in HashiCorp Vault Lookup Credential
    debug: 
      msg: 
        - "username : {{ ansible_user }}"
        - "password : {{ ansible_password }}"
    delegate_to: 127.0.0.1 

  - name: Setting host data using data in HashiCorp Vault Secret Lookup
    set_fact:
      vault_data: "{{ vaultkv_secret }}" 
    delegate_to: 127.0.0.1

  - name: Print secret information using data in HashiCorp Vault Lookup Credential
    debug: 
      msg: 
        - "lookup data all : {{ vault_data }}"  
        - "lookup data say : {{ vault_data.say }}"  
    delegate_to: 127.0.0.1 

#  - name: Ping to Host
#    ping: 
```
