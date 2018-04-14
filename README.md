Certbot NGINX
=========

Simple Ansible role to install `certbot` with NGINX plugin on **Ubuntu 16.04**.

This role will:
1. Add `certbot` PPA repository
2. Install `letsencrypt` and `python-certbot-certbot-nginx` packages
3. `letsencrypt` package will add a `renew` cron job and a systemd-timer ([More info](https://certbot.eff.org/#ubuntuxenial-nginx)
4. Generate a Let's Encrypt SSL certificate for the given `domain_name`

Role Variables
--------------
```yaml
domain_name: www.mydomain.io
letsencrypt_email: myaccount@letsencrypt.org
```

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
    - role: coopdevs.certbot-nginx
      domain_name: www.mydomain.io
      letsencrypt_email: myaccount@letsencrypt.org
```

Let's Encrypt Staging Environment
---------------------------------

This role includes `letsencrypt_staging` variable which defaults to `no`. For development or debugging purposes, one can set it to `yes`,
for example by [Passing Variables On The Command Line](http://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#passing-variables-on-the-command-line) `--extra-vars "letsencrypt_staging=yes"`

This will result in use of [Let's Encrypt Staging Environment](https://letsencrypt.org/docs/staging-environment/) and reducing chance of
running up agains rate limits.

License
-------

BSD

Author Information
------------------

Coopdevs http://coopdevs.org
