# Ansible Role to install extra repository sources

[![Build Status][travis-build-status]][travis-tests]

Installs extra repository sources on Debian/Ubuntu servers.

**Important!** Make sure you check if your distribution and release is supported. Click the links below to see the most up-to-date availability.

Available out of the box:
- [Dotdeb][setup-dotdeb] (wheezy, jessie)
- [MariaDB][setup-mariadb] (wheezy, jessie, stretch, sid, precise, trusty, xenial, yakkety)
- [MySQL][setup-mysql] (wheezy, jessie, precise, trusty, utopic, vivid, xenial)
- [Nginx][setup-nginx] (wheezy, jessie, stretch, precise, trusty, xenial, yakkety)
- [PHP 7.1][setup-php71] (jessie, stretch)
- [PostgreSQL][setup-postgresql] (wheezy, jessie, stretch, precise, trusty, xenial)
- [Tor][setup-tor] (wheezy, jessie, stretch, sid, precise, trusty, xenial)

Easily install and remove keys and repositories using the `apt_extra_sources_keys` and `apt_extra_sources_repos` variables.

## Requirements

GnuPG, which can be installed using `apt-get install gnupg` (or see `tests/test.yml`).

## Role Variables

See the [`defaults/main.yml`][defaults] file for more details.
All key and repository paths can be overridden.

Main variables:

```yaml
# Pre-packaged
apt_extra_sources_mariadb: yes
apt_extra_sources_mysql: yes
apt_extra_sources_mysql_version: 5.7 # can be either 5.6 or 5.7
apt_extra_sources_nginx: yes
apt_extra_sources_php71: yes
apt_extra_sources_tor: yes

# Modify pre-packaged
apt_extra_sources_tor_repo: "deb http://deb.torproject.org/torproject.org tor-experimental-0.3.2.x-stretch main"

# Manually add
apt_extra_sources_keys:
  - url: "https://www.dotdeb.org/dotdeb.gpg"
  - { keyserver: keyserver.ubuntu.com, id: F1656F24C74CD1D8 }
apt_extra_sources_repos:
  - repo: "deb http://packages.dotdeb.org jessie all"
  - repo: "deb http://mirror.rackspeed.de/mariadb.org/repo/10.2/debian stretch main"

# Manually remove
apt_extra_sources_keys:
  - { url: "https://www.dotdeb.org/dotdeb.gpg", state: absent }
apt_extra_sources_repos:
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
    - role: noplanman.apt-extra-sources
```

## License

MIT

[travis-build-status]: https://travis-ci.org/noplanman/ansible-role-apt-extra-sources.svg?branch=master "Travis-CI Build Status"
[travis-tests]: https://travis-ci.org/noplanman/ansible-role-apt-extra-sources "Travis-CI Tests"
[defaults]: https://github.com/noplanman/ansible-role-apt-extra-sources/blob/master/defaults/main.yml "Default variables"
[setup-dotdeb]: https://www.dotdeb.org/instructions/ "Setup Dotdeb repository"
[setup-mariadb]: https://downloads.mariadb.org/mariadb/repositories/ "Setup MariaDB repository"
[setup-mysql]: https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/#repo-qg-apt-repo-manual-setup "Setup MySQL repository"
[setup-nginx]: https://nginx.org/en/linux_packages.html#stable "Setup Nginx repository"
[setup-php71]: https://packages.sury.org/php/README.txt "Setup PHP 7.1 repository"
[setup-postgresql]: https://www.postgresql.org/download/linux/ "Setup PostgreSQL"
[setup-tor]: https://www.torproject.org/docs/debian.html.en "Setup Tor repository"
