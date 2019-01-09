Certbot NGINX
=========

Simple Ansible role to install `certbot` with NGINX plugin on **Ubuntu 16.04**.

This role will:
1. Add `certbot` PPA repository
2. Install `certbot` and `python-certbot-nginx` packages
3. `certbot` package will add a `renew` cron job and a systemd-timer ([More info](https://certbot.eff.org/#ubuntuxenial-nginx)
4. Generate a Let's Encrypt SSL certificate for the given `domain_name`

Role Variables
--------------
```yaml
domain_name: www.mydomain.io
letsencrypt_email: myaccount@letsencrypt.org
certbot_nginx_cert_name: mycert # optional
```

if set, `certbot_nginx_cert_name`'s value will be passed to the certbot's `--cert-name` argument, which is used to identify the certificate in certbot command such as `certbot delete`. You will see a list of certificates identified with this name by running `certbot certificates`. This name will also be used as the file paths for the certificate in `/etc/letsencrypt/live/`.

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
    - role: coopdevs.certbot-nginx
      domain_name: www.mydomain.io
      letsencrypt_email: myaccount@letsencrypt.org
      certbot_nginx_cert_name: mycert
```

Let's Encrypt Staging Environment
---------------------------------

This role includes `letsencrypt_staging` variable which defaults to `no`. For development or debugging purposes, one can set it to `yes`,
for example by [Passing Variables On The Command Line](http://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#passing-variables-on-the-command-line) `--extra-vars "letsencrypt_staging=yes"`

This will result in use of [Let's Encrypt Staging Environment](https://letsencrypt.org/docs/staging-environment/) and reducing chance of
running up against rate limits.

License
-------

BSD

Author Information
------------------

Coopdevs http://coopdevs.org
