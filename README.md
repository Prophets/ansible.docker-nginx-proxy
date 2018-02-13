Role Name
=========

Systemd service for [jwilder/nginx](https://github.com/jwilder/nginx-proxy) docker container and optional [docker-letsencrypt-nginx-proxy-companion](https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion).

Requirements
------------

Any OS capable of running Docker and systemd.

Role Variables
--------------

#### Proxy container configuration

The name to use for running the container.

    docker_proxy_container_name: nginx_proxy

Configuration path for "proxy-wide" settings. See [Proxy-wide configuration](https://github.com/jwilder/nginx-proxy#proxy-wide).

    docker_proxy_wide_config_path: /usr/local/etc/nginx_proxy_wide.conf

The configuration to put in the "proxy-wide" configuration. To disable and use a custom config file with `docker_proxy_wide_config_path` set this variable to a falsy boolean value.

    docker_proxy_wide_config: |
      client_max_body_size 100m;

Optional directory path with basic authentication configurations. See [Basic Authentication Support](https://github.com/jwilder/nginx-proxy#basic-authentication-support).

    docker_proxy_htpasswd_dir_path: /usr/local/etc/nginx_proxy/htpasswd

Optional directory path with SSL certificates. See [SSL support](https://github.com/jwilder/nginx-proxy#ssl-support).

    docker_proxy_certs_dir_path: /usr/local/etc/nginx_proxy/certs

Optional directory path with virtual host configurations. See [Per virtual host configuration](https://github.com/jwilder/nginx-proxy#per-virtual_host-default-configuration) and [Per virtual host location configuration](https://github.com/jwilder/nginx-proxy#per-virtual_host-location-default-configuration).

    docker_proxy_vhosts_dir_path: /usr/local/etc/nginx_proxy/vhosts

Use the Let's Encrypt companion container.

    docker_use_letsencrypt_companion: yes

The name to use for running the Let's Encrypt companion container.

    docker_letsencrypt_companion_container_name: letsencrypt_proxy_companion

#### Systemd service unit names

Location to place the systemd init configuration.

    docker_proxy_service_systemd: /etc/systemd/system

Systemd service name for the proxy service.

    docker_proxy_service_name: nginx_proxy

Systemd service name for the  Let's Encrypt companion service.

    docker_letsencrypt_companion_service_name: letsencrypt_proxy_companion

Dependencies
------------

- geerlingguy.docker

Example Playbook
----------------

    - hosts: dockerhosts
      become: yes
      roles:
        - name: prophets.docker-proxy

License
-------

BSD

Author Information
------------------

Stijn Huyberechts for [prophets.be](https://prophets.be)