Wordpress Hosting
=================

Development Environment
-----------------------
The official [WordPress instructions](http://codex.wordpress.org/Installing_WordPress).

First point a web browser at `http://192.168.1.100/phpmyadmin` (where
192.168.1.100 should be replaced with the IP address of your running VM) and
create the MySQL table for the WordPress install.

Then edit the wp-config.php file in the root of the wordpress application
directory to look like `wordpress/wp-config.php` in this repository.

To deploy, use the `bin/deploy_apache_app` script in this repository. Don't
forget to preface the command with `su` like this:

    sudo su www-data bin/deploy_apache_app path/to/wordpress/app
