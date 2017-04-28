# Ansible Role to install extra repository sources

[![Build Status][travis-build-status]][travis-tests]

Installs extra repository sources on Debian/Ubuntu servers.

Available out of the box:
- [MariaDB][setup-mariadb]
- [MySQL][setup-mysql]
- [Nginx][setup-nginx]
- [PHP 7.1][setup-php71]
- [Tor][setup-tor]

Easily install and remove keys and repositories using the `extra_sources_keys` and `extra_sources_repos` variables.

## Requirements

None.

## Role Variables

See the [`defaults/main.yml`][defaults] file for more details.
All key and repository paths can be overridden.

Main variables:

```yaml
# Pre-packaged
extra_sources_mariadb: yes
extra_sources_mysql: yes
extra_sources_mysql_version: 5.7 # can be either 5.6 or 5.7
extra_sources_nginx: yes
extra_sources_php71: yes
extra_sources_tor: yes

# Manually add
extra_sources_keys:
  - url: "https://www.dotdeb.org/dotdeb.gpg"
  - { keyserver: keys.gnupg.net, id: A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89 }
extra_sources_repos:
  - repo: "deb http://packages.dotdeb.org jessie all"
  - repo: "deb http://deb.torproject.org/torproject.org jessie main"

# Manually remove
extra_sources_keys:
  - { url: "https://www.dotdeb.org/dotdeb.gpg", state: absent }
extra_sources_repos:
  - { repo: "deb http://packages.dotdeb.org jessie all", state: absent }
```

## Dependencies

None.

## Example Playbook

```yaml
---
- hosts: servers
  become: yes
  roles:
    - role: noplanman.extra-sources
```

## License

MIT

[travis-build-status]: https://travis-ci.org/noplanman/ansible-extra-sources.svg?branch=master "Travis-CI Build Status"
[travis-tests]: https://travis-ci.org/noplanman/ansible-extra-sources "Travis-CI Tests"
[defaults]: https://travis-ci.org/noplanman/ansible-extra-sources/blob/master/defaults/main.yml "Default variables"
[setup-mariadb]: https://downloads.mariadb.org/mariadb/repositories/ "Setup MariaDB repository"
[setup-mysql]: https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/#repo-qg-apt-repo-manual-setup "Setup MySQL repository"
[setup-nginx]: https://nginx.org/en/linux_packages.html#stable "Setup Nginx repository"
[setup-php71]: https://packages.sury.org/php/README.txt "Setup PHP 7.1 repository"
[setup-tor]: https://www.torproject.org/docs/debian.html.en "Setup Tor repository"
