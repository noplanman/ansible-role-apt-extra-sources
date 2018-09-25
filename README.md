# Ansible Role to install extra repository sources

[![Build Status][travis-build-status]][travis-tests] [![Ansible Role][ansible-role-shield]][ansible-role]

---

:rocket: Development has moved to **[git.feneas.org]**.

(The repository on GitHub is only a mirror, so fork on Feneas to contribute. No registration needed, just sign in with your GitHub account.)

---

Installs extra repository sources on Debian/Ubuntu servers.

**Important!** Make sure you check if your distribution and release is supported. Click the links below to see the most up-to-date availability.

Available out of the box:
- [Dotdeb][setup-dotdeb]
- [MariaDB][setup-mariadb]
- [MySQL][setup-mysql]
- [Nginx][setup-nginx]
- [PHP 7.1][setup-php71]
- [PostgreSQL][setup-postgresql]
- [Tor][setup-tor]

Easily install and remove keys and repositories using the `apt_extra_sources_keys` and `apt_extra_sources_repos` variables.

## Requirements

None.

## Role Variables

See the [`defaults/main.yml`][defaults] file for more details.
All key and repository paths can be overridden.

Main variables:

```yaml
# Pre-packaged
apt_extra_sources_mariadb: yes
apt_extra_sources_mysql: yes
apt_extra_sources_mysql_version: 5.7 # can be either 5.6, 5.7 or 8.0
apt_extra_sources_nginx: yes
apt_extra_sources_php71: yes
apt_extra_sources_tor: yes

# Modify pre-packaged
apt_extra_sources_tor_repo: "deb http://deb.torproject.org/torproject.org tor-experimental-0.3.5.x-stretch main"

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
    - role: noplanman.apt_extra_sources
```

## Tests

Docker is used to test the role with different operating systems.

Check the [`tests`] folder.

## License

MIT

[travis-build-status]: https://img.shields.io/travis/noplanman/ansible-role-apt-extra-sources.svg?style=flat-square "Travis-CI Build Status"
[travis-tests]: https://travis-ci.org/noplanman/ansible-role-apt-extra-sources "Travis-CI Tests"
[ansible-role-shield]: https://img.shields.io/ansible/role/30052.svg?style=flat-square "Apt Extra Sources on Ansible Galaxy"
[ansible-role]: https://galaxy.ansible.com/noplanman/apt_extra_sources "Apt Extra Sources on Ansible Galaxy"
[git.feneas.org]: https://git.feneas.org/noplanman/ansible-role-apt-extra-sources "Ansible Role Apt Extra Sources on Feneas"
[setup-dotdeb]: https://www.dotdeb.org/instructions/ "Setup Dotdeb repository"
[setup-mariadb]: https://downloads.mariadb.org/mariadb/repositories/ "Setup MariaDB repository"
[setup-mysql]: https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/#repo-qg-apt-repo-manual-setup "Setup MySQL repository"
[setup-nginx]: https://nginx.org/en/linux_packages.html#stable "Setup Nginx repository"
[setup-php71]: https://packages.sury.org/php/README.txt "Setup PHP 7.1 repository"
[setup-postgresql]: https://www.postgresql.org/download/linux/ "Setup PostgreSQL repository"
[setup-tor]: https://www.torproject.org/docs/debian.html.en "Setup Tor repository"
[defaults]: https://git.feneas.org/noplanman/ansible-role-apt-extra-sources/blob/master/defaults/main.yml "Default variables"
[`tests`]: https://git.feneas.org/noplanman/ansible-role-apt-extra-sources/tree/master/tests "Tests"
