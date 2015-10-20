Ansible config for PHP web dev
=================

Simple config for PHP web development local VM. Based on config from [Phansible](http://phansible.com) generator.

Installation
-------------

Just download tarball or make git clone, enter the directory with files and run:

```
vagrant up
```

Features
-------------

* Ubuntu Trusty Tahr (14.04) x64 base box
* 1024 MB RAM / 1 CPU
* Hostname: `webdev.local`
* IP address: `192.168.56.101`
* Forwarded ports (Guest => Host):
    * 22 => 2222 (Vagrant default)
    * 3306 => 3307 (for MySQL)
    * 5432 => 5433 (for PostgreSQL)
* Nginx with ability to set several additional virtual hosts
* MySQL (latest available from Ubuntu repo)
* PostgreSQL 9.4 (from official repo)
* MongoDB (latest available from official repo)
* Redis 2.8.19 (as selected by Phansible)
* PHP 5.6 with XDebug (from PPA `ondrej/php5-5.6`)
* Composer (available from console as `composer`)
* XHProf (URL address: `http://webdev.local/xhprof/xhprof_html`)
* Adminer DB Tool (URL address: `http://webdev.local/adminer`)

_Note:_ you can connect to MySQL/PostgreSQL from any apps outside of the VM without SSH tunneling:
* MySQL: host=localhost, port=3307, user=dbuser, password=dbuser
* PostgreSQL: host=localhost, port=5433, user=dbuser, password=dbuser

This is useful for developers who using Windows as host OS (like me).

Configuring
-------------

Feel free to change any config options in `Vagrantfile`, `vars/all.yml`.
If you want to add more virtual hosts, update `vhosts` section in `nginx` (`vars/all.yml`). Example for `test.local`:

```yaml
nginx:
    docroot: /var/www/html
    servername: webdev.local
    vhosts: [
      { servername: test.local, docroot: /var/www/test.local/www },
    ]
```

Do not forget to update `hosts` file on your host OS.

PHP options are available in section `php.options`. XDebug options - in section `xdebug.settings`

After all changes made run next command to apply them to the VM.

```
vagrant provision
```

Useful links
-------------

* [Vagrant](https://www.vagrantup.com)
* [Ansible](http://www.ansible.com)
* [Phansible](http://phansible.com)
* [Adminer](https://www.adminer.org)

Author
-------------

Copyright (c) 2015 by Stevad.
