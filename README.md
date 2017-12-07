#Ansible Role: JSMin#

Build and install the latest version of the [jsmin PHP Extension](https://github.com/sqmk/pecl-jsmin/) on any Ubuntu/Debian based system.
This extension provides a fast JavaScript minification function.

##Requirements##

- Debian (8+)/Ubuntu(10+)
- Git. A role such as [geerlingguy.git](https://galaxy.ansible.com/geerlingguy/git/) can supply this.
- PHP (5.6+)
- PHP Development headers installed for each PHP version you want to target.

##Role Variables##

The following two variables are defined in defaults/main.yml and will be over-written by any variables defined basically anywhere else with the same name

    jsmin_php_version

The PHP version to target with this build/install. If not provided, will attempt to select your primary version.

    jsmin_clone_dest: ~/git/jsmin

The location that jsmin will be cloned to for building.

    jsmin_enable: true

Whether or not to enable the jsmin module after building & installing.

    jsmin_path_ini: /etc/php/{{ jsmin_php_version }}/mods-available/jsmin.ini

The ini path to use to create the jsmin.ini if enabling jsmin.

    jsmin_path_php: php{{ jsmin_php_version }}

The path to the php-config binary.

    jsmin_path_phpconfig: php-config{{ jsmin_php_version }}

The path to the php-config binary.

    jsmin_path_phpize: phpize{{ jsmin_php_version }}

The path to the phpize binary.

    jsmin_path_phpenable: phpenable -v {{ jsmin_php_version }}

The path to the phpenable binary.

###Debian 8 with PHP 5.6###
The default paths with Debian 8 and PHP 5.6 are different than on Ubuntu and Debian 9. To seamlessly account for this, the main task checks if the generic path doesn't exist. If the path doesn't exist, it imports the variables from `vars/debian.yml`

##Example Playbook##

To  install `jsmin` for just your primary PHP version:

    - hosts: all
      roles:
        -role: nickwilde1990.jsmin

To install `jsmin` for multiple PHP versions.

    - hosts: all
      tasks:
      - include_role:
        name: nickwilde1990.jsmin
      with_items:
        - 7.0
        - 7.1
      loop_control:
        loop_var: jsmin_php_version

##License##

MIT

##Author Information##

Nick Wilde ([BriarMoon Design](https://design.briarmoon.ca))
