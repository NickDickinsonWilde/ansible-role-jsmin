Ansible Role: JSMin
=========

Build and install the [jsmin PHP Extension](https://github.com/sqmk/pecl-jsmin/) on any Ubuntu or (probably) Debian based system.
This extension provides a fast JavaScript minification function.

Requirements
------------

- Debian/Ubuntu
- Git. A role such as [geerlingguy.git](https://galaxy.ansible.com/geerlingguy/git/) can supply this.
- PHP (5.6)
- PHP Development headers installed for any PHP version(s) you want to target.


Role Variables
--------------

The following two variables are defined in defaults/main.yml and will be over-written by any variables defined basically anywhere else with the same name

    jsmin_php_version

The PHP version to target with this build/install. If not provided, will attempt to select your primary version.

    jsmin_clone_dest: ~/git/jsmin

The location that jsmin will be cloned to for building.

    jsmin_enable: true

Whether or not to enable the jsmin module after building & installing.

Then there are a bunch of path variables. These path variables change depending on OS and are defined in `vars/*.yml`. They are not easily over-written.

    jsmin_path_ini: /etc/php/{{ jsmin_php_version }}/mods-available/jsmin.ini # Ubuntu
    jsmin_path_ini: /etc/php5/mods-available/jsmin.ini # Debian 8

The ini path to use to create the jsmin.ini if enabling jsmin.

    jsmin_path_phpconfig: php-config{{ jsmin_php_version }} # Ubuntu
    jsmin_path_phpconfig: php-config5 # Debian 8

The path to the php-config binary.

    jsmin_path_phpize: phpize{{ jsmin_php_version }} # Ubuntu
    jsmin_path_phpize: phpize5 # Debian 8

The path to the phpize binary.

    jsmin_path_phpenable: phpenable -v {{ jsmin_php_version }}# Ubuntu
    jsmin_path_phpenable: php5enable # Debian 8

The path to the phpenable binary.

Example Playbook
----------------

To  install `jsmin` for just your primary PHP version:

    - hosts: all
      roles:
        -role: nickwilde1990.jsmin

To install `jsmin` for multiple PHP versions. Note: this will probably not work on Debian 8 but will work fine on Ubuntu.

    - hosts: all
      tasks:
      - include_role:
        name: nickwilde1990.jsmin
      with_items:
        - 7.0
        - 7.1
      loop_control:
        loop_var: jsmin_php_version

License
-------

MIT

Author Information
------------------

Nick Wilde ([BriarMoon Design](https://design.briarmoon.ca))