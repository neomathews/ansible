Role Name
=========

Este role lo que hace es cambiar al clave root.

Requirements
------------

El unico requerimiento es que sapan lo que estan haciendo.

Role Variables
--------------

Deben de crear un archivo en vars (roles/password/vars/root.yml) en donde archivaran la clave root en texto plano. Deben de tener claro que por propositos de entrenamiento este archivo no ha sido protegido con ansible-vault
Vean el formato del mismo para un mejor entendimiento.
Tambien lo puedes combinar con diferenctes entornos, ejemplo de esto seria:
---
password:
  prod: 'PasswORD-AQUI'
  qa1: 'AQUI-EL-PassworD'

Y en el playbook, solo especificar de la siguiente forma:

    password:        "{{ password[working_environment]|password_hash('md5') }}"

Donde working_environment debe de estar declarado como variable global en sus archivos de inventario u otro lugar

Dependencies
------------

No creo que exista alguna dependencia

Example Playbook
----------------


---
# Update a user password
# Requires user_name as an extra var
# example --extra-vars="user_name=svc_ansible"
- hosts: all
  name: Set user password
  become: "{{ use_sudo|default(True) }}"
  gather_facts: False
  roles:
    - password

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).

