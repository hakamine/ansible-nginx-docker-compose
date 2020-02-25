ansible-nginx-docker-compose
============================

Ansible role to deploy nginx on a container managed by docker-compose.
Nginx is configured to use SSL/TLS using a self signed certificate or a
Let's Encrypt certificate (obtained with certbot).

Requirements
------------

None

Role Variables
--------------

See [`defaults/main.yml`](./defaults/main.yml)

Dependencies
------------

None

Example Playbook
----------------

To deploy nginx with a self-signed certificate (role default):
```yaml
- hosts: 
    - myhost.com
  roles:
    - role: "ansible-nginx-docker-compose"
        become: "yes"
        tags:
          - "nginxdc"
```

To deploy nginx with Let's Encrypt (DNS for the host must be
configured beforehand):
```yaml
- hosts: 
    - myhost.com
  vars:
    nginxdc_le_enable: yes
    nginxdc_le_domains:
      - myhost.com
    nginxdc_le_email: myemail@myemaildomain.com
    nginxdc_nginx_conf_d_templates:
      - "nginx/conf.d/default-tls.conf"
    nginxdc_nginx_template_default_ssl_cert : "/etc/letsencrypt/live/myhost.com/fullchain.pem"
    nginxdc_nginx_template_default_ssl_cert_key : "/etc/letsencrypt/live/myhost.com/privkey.pem"

  roles:
    - role: "ansible-nginx-docker-compose"
        become: "yes"
        tags:
          - "nginxdc"

```

License
-------

BSD

Author Information
------------------

Artefactual Systems
