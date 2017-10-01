mebooks.ansible-role-docker-traefik
===================================

Based on [rgarrigue.docker-traefik](https://github.com/rgarrigue/ansible-role-docker-traefik).

Installs the [Traefik](https://traefik.io/) reverse proxy via Docker.

Data is under `/etc/traefik`

Requirements
------------

Developped and tested on *Ubuntu Server 16.10 Yakkety*, should work on other OSes.

It's running on Docker.

Role Variables
--------------

For let's encrypt certificate, and automatic reverse proxy

- `domain` defaults to *domain.tld*
- `owner`  defaults to *admin*
- `email`  defaults to *whoever@example.com*

- `users.username` defaults to *admin*
- `users.password` defaults to *My own little 1 cloud !*
- `users.acl` defaults to *traefik*

Dependencies
------------

- `mebooks.ansible-role-docker-traefik`

Example Playbook
----------------

```yml
- hosts: remote
  remote_user: deploy
  become: true
  become_user: root
  become_method: sudo

  vars:
    traefik_testing: true
    owner: administrator
    domain: mebooks.co.nz
    email: mebooks.support@gmail.com
    users:
     # owner_password / owner_password_encrypted are defined in the unversioned group_vars/droplets
    - username: "{{ owner }}"
      password: "{{ owner_password }}"
      acl:
      - traefik

  roles:
    # We presume we've already run ansible-role-users and ansible-role-common
    # The following role is listed as dependencies in ansible-role-docker-traefik/meta/main.yml:
    # - role: ansible-role-docker
    - role: ansible-role-docker-traefik
```

License
-------

GPLv3

Author Information
------------------

Jason Darwin
