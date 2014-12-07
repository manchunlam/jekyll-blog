---
layout: post
title: "CentOS Setup (Part IX) - Configure apache"
date: 2014-05-03 11:25:39 -0400
comments: true
categories: centos
---

You should log in as `root`.

1. Enable _Virtual Host_

    ```sh
    vi /etc/httpd/conf/httpd.conf
    # find and uncomment the following line:
    #
    # #Include /etc/httpd/conf/extra/httpd-vhosts.conf
    ```
<!-- more -->
2. Create `vhosts` directory to house configuration for each domain/subdomain

    ```
    cd /etc/httpd/conf/
    mkdir vhosts

    cd vhosts
    touch example.config # for example.com
    touch foo.example.conf # for foo.example.com
    ```

3. Tell `apache` where the `vhost`s are

    ```
    vi /etc/httpd/conf/extra/httpd-vhosts.conf
    # comment out all the `VirtualHost` examples

    # add "Include /etc/httpd/conf/vhosts/*.conf" to end of file
    ```

4. Edit a `vhost` file

    ```
    vi /etc/httpd/conf/vhosts/example.config
    ```

    Add the following to the file

    ```
    <Directory "/home/someuser/projects/blog/public">
        Order allow,deny
        Allow from all
        # New directive needed in Apache >= 2.4.3:
        Require all granted
    </Directory>

    <VirtualHost *:80>
        DocumentRoot "/home/someuser/projects/blog/public"
    </VirtualHost>
    ```

    For an explanation in details regarding `Directory`, see this excellent
    [post](http://stackoverflow.com/a/13923435).

    The `/home/someuser/projects/blog/public` directory should contain at least
    an `index.html` file. For example

    ```
    <h1>Testing!</h1>
    ```

5. Test for errors in configuration files

    ```
    httpd -S
    ```

    Make sure there are no errors in the output.

5. Allow `apache` to enter your user's directory

    By default, `apache` runs with the `User` and `Group` `daemon`. This
    `daemon` user probably cannot enter your user's `HOME` directory.

    To enable `apache` to _search_ and display your user's content, we will
    add user `daemon` to the target user's `group`, and grant `execute` (or
    _search_) privilege to the group, on the relevant directories.

    For a good explanation on `execute` (`x`) permissions, please see these
    2 posts.

      1. [On execute permission](http://stackoverflow.com/a/11266203)
      2. [On all permissions](http://unix.stackexchange.com/a/21252)

    ```sh
    usermod -a -G someuser daemon # add user "daemon" to the group "someuser"

    chmod g+x /home/someuser
    # give the group "someuser" search privilege on /home/someuser
    ```

    Note:

    99% of the time, all directories under /home/someuser already have
    read, and search, privileges for the group "someuser"

    If after server restart, apache still can't see your file, you're the 1%.
    Check the permissions on relevant directories and files, and redo `chmod`
    for them.

6. Test!

    ```
    service httpd restart
    ```

    Use a browser to go to your IP address, or domain, you should see the
    `index.html` you created.
