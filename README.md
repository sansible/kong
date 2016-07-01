# Kong

Master: [![Build Status](https://travis-ci.org/sansible/kong.svg?branch=master)](https://travis-ci.org/sansible/kong)  
Develop: [![Build Status](https://travis-ci.org/sansible/kong.svg?branch=develop)](https://travis-ci.org/sansible/kong)

* [ansible.cfg](#ansible-cfg)
* [Installation and Dependencies](#installation-and-dependencies)
* [Tags](#tags)
* [Examples](#examples)

This role installs Kong on Debian systems, configured to use Postgres for storage (as opposed to Cassandra).

For more information on Kong please visit [getkong](https://getkong.org/).




## ansible.cfg

This role is designed to work with merge "hash_behaviour". Make sure your
ansible.cfg contains these settings

```INI
[defaults]
hash_behaviour = merge
```




## Installation and Dependencies

To install run `ansible-galaxy install sansible.kong` or add this to your
`roles.yml`, you can use `sansible.postgres` for installing postgres.

```YAML
- name: sansible.kong
  version: v1.0
```

and run `ansible-galaxy install -p ./roles -r roles.yml`




## Tags

This role uses two tags: **build** and **configure**

* `build` - Installs Kong and all it's dependencies.
* `configure` - Configure and ensures that the Kong service is running.




## Examples

To install:

```YAML
- name: Install and configure Kong
  hosts: "somehost"

  roles:
    - role: sansible.kong
      kong:
        db:
          host: localhost
          name: kong
          password: kong
          root_password: rootpassword
          port: 5432
          user: kong
          root_user: rootuser
```

All options:

```YAML
- name: Install and configure Kong
  hosts: "somehost"

  roles:
    - role: sansible.kong
      kong:
        admin_api_listen: "0.0.0.0:8001"
        db:
          host: localhost
          name: kong
          password: kong
          root_password: ~
          port: 5432
          user: kong
          root_user: ~
        dependencies:
          - dnsmasq
          - libpcre3
          - lua5.2
          - luarocks
          - netcat
          - openssl
          - procps
          - python-psycopg2
        logs:
          # combined or json
          access_log_format: combined
        plugins:
          - acl
          - basic-auth
          - cors
          - file-log
          - hmac-auth
          - http-log
          - ip-restriction
          - jwt
          - key-auth
          - galileo
          - oauth2
          - rate-limiting
          - response-ratelimiting
          - response-transformer
          - request-size-limiting
          - request-transformer
          - ssl
          - tcp-log
          - udp-log
        proxy_listen: "0.0.0.0:8000"
        proxy_listen_ssl: "0.0.0.0:8443"
        version: 0.8.3
```
