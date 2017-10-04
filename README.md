PHP-FPM
=======

[![Build Status](https://travis-ci.org/injectedMonkey/ansible-role-php-fpm.svg?branch=master)](https://travis-ci.org/injectedMonkey/ansible-role-php-fpm)
[![License](https://img.shields.io/badge/License-BSD%202--Clause-orange.svg)](https://opensource.org/licenses/BSD-2-Clause)
[![GitHub release](https://img.shields.io/github/release/injectedMonkey/ansible-role-php-fpm.svg?style=flat)](https://github.com/injectedMonkey/ansible-role-php-fpm/releases)

Ansible role for php-fpm. It's designed for my development environment
but might reach sometimes production ready state.

Supported distributions:
- Debian
- Ubuntu


Supported php versions:
- 5.6
- 7.0
- 7.1


Requirements
------------

This role requires ansible >= 2.4.

Dictionaries are used for configuration. Partially overriding defaults needs
      hash_behaviour = merge
set in your ansible.cfg or
      ANSIBLE_HASH_BEHAVIOUR=merge
for your environment.

Role Variables
--------------

      php:
        version: 7.1
        repositories:
          ppa:
            - ppa:ondrej/php
          deb:
            - { key: "https://packages.sury.org/php/apt.gpg",
                repo: "deb http://packages.sury.org/php/ {{ ansible_distribution_release }} main",
                filename: php }
        dependencies:
          - apt-transport-https
        packages:
          - cli
          - curl
          - fpm
          - intl
          - mysql
          - xml
        ini:
          fpm:
            - { section: Date, option: date.timezone, value: Europe/Berlin }
            - { section: PHP, option: max_execution_time, value: 60 }
            - { section: PHP, option: memory_limit, value: 512M }
          cli:
            - { section: Date, option: date.timezone, value: Europe/Berlin }
            - { section: PHP, option: max_execution_time, value: 0 }
            - { section: PHP, option: memory_limit, value: 512M }



Dependencies
------------

None.


Example Playbook
----------------

    - hosts: servers
    - include_role:
        name: injectedMonkey.php-fpm
      vars:
        php:
          version: 7.1
          repositories:
            ppa:
              - ppa:ondrej/php
            deb:
              - { key: "https://packages.sury.org/php/apt.gpg",
                repo: "deb http://packages.sury.org/php/ {{ ansible_distribution_release }} main",
                filename: php }
          dependencies:
            - apt-transport-https
          packages:
            - cli
            - curl
            - fpm
            - intl
            - mysql
            - xml
          ini:
            fpm:
              - { section: Date, option: date.timezone, value: Europe/Berlin }
              - { section: PHP, option: max_execution_time, value: 60 }
              - { section: PHP, option: memory_limit, value: 512M }
            cli:
              - { section: Date, option: date.timezone, value: Europe/Berlin }
              - { section: PHP, option: max_execution_time, value: 0 }
              - { section: PHP, option: memory_limit, value: 512M }

License
-------

BSD

Author Information
------------------

injectedMonkey.wtf
