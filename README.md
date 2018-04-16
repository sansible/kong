# Kong

Master: [![Build Status](https://travis-ci.org/sansible/kong.svg?branch=master)](https://travis-ci.org/sansible/kong)  
Develop: [![Build Status](https://travis-ci.org/sansible/kong.svg?branch=develop)](https://travis-ci.org/sansible/kong)

* [Installation and Dependencies](#installation-and-dependencies)
* [Tags](#tags)
* [Examples](#examples)

This role installs Kong on Debian systems, configured to use Postgres for
storage (as opposed to Cassandra).

For more information on Kong please visit [getkong](https://getkong.org/).


## Installation and Dependencies

To install run `ansible-galaxy install sansible.kong` or add this to your
`roles.yml`, you can use `sansible.postgres` for installing postgres.

```YAML
- name: sansible.kong
  version: v2.0
```

and run `ansible-galaxy install -p ./roles -r roles.yml`


## Tags

This role uses two tags: **build** and **configure**

* `build` - Installs Kong and all its dependencies.
* `configure` - Configure and ensures that the Kong service is running.


## Examples

To install:

```YAML
- name: Install and configure Kong
  hosts: "somehost"

  roles:
    - role: sansible.kong
      sansible_kong_db_host: localhost
      sansible_kong_db_name: kong
      sansible_kong_db_password: kong
      sansible_kong_db_root_password: rootpassword
      sansible_kong_db_port: 5432
      sansible_kong_db_user: kong
      sansible_kong_db_root_user: rootuser
```

All options:

```YAML
- name: Install and configure Kong
  hosts: "somehost"

  roles:
    - role: sansible.kong
      sansible_kong_admin_api_listen: "0.0.0.0:8001"
      sansible_kong_db_host: localhost
      sansible_kong_db_name: kong
      sansible_kong_db_password: kong
      sansible_kong_db_root_password: ~
      sansible_kong_db_port: 5432
      sansible_kong_db_user: kong
      sansible_kong_db_root_user: ~
      sansible_kong_dependencies:
        - dnsmasq
        - libpcre3
        - lua5.2
        - luarocks
        - netcat
        - openssl
        - procps
        - python-psycopg2
      sansible_kong_access_log_format: combined
      sansible_kong_proxy_listen: "0.0.0.0:8000"
      sansible_kong_proxy_listen_ssl: "0.0.0.0:8443"
      sansible_kong_version: 0.9.3
```
