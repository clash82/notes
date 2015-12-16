---
layout: default
title: eZ Platform (MacOS X clean install)
---

This guide allows you to prepare environment required to install `eZ Platform v1` on `MacOS X Yosemite` (this guide is incompatible with `eZ Publish Platform 5.4` and all `eZ Platform beta releases`).

## 1. Install MySQL: ##

Download and install MySQL from the <a href="http://dev.mysql.com/downloads/mysql/" target="_blank">official website</a> (eg. mysql-5.6.26-osx10.9-x86_64.dmg).

## 2. Setup PHP: ##

Edit Apache 2 configuration file:

{% highlight bash %}
sudo vi /private/etc/apache2/httpd.conf
{% endhighlight %}

Uncomment/modify following lines:

{% highlight apacheconf %}
LoadModule php5_module libexec/apache2/libphp5.so
{% endhighlight %}

Create new `php.ini` file base on defaults:

{% highlight bash %}
sudo cp /private/etc/php.ini.default /private/etc/php.ini
{% endhighlight %}

Edit `php.ini`:

{% highlight bash %}
sudo vi /private/etc/php.ini
{% endhighlight %}

and uncomment/modify following lines:

{% highlight ini %}
date.timezone = "Europe/Warsaw"
{% endhighlight %}

(...)

{% highlight ini %}
pdo_mysql.default_socket  = /tmp/mysql.sock
{% endhighlight %}

Increase `memory_limit` value for eZ Platform:

{% highlight ini %}
memory_limit = 4G
{% endhighlight %}

## 3. Setup virtual host and start Apache 2: ##

Edit Apache 2 configuration file:

{% highlight bash %}
sudo vi /private/etc/apache2/httpd.conf
{% endhighlight %}

Uncomment/modify following lines:

{% highlight apacheconf %}
LoadModule vhost_alias_module libexec/apache2/mod_vhost_alias.so
{% endhighlight %}

(...)

{% highlight apacheconf %}
LoadModule rewrite_module libexec/apache2/mod_rewrite.so
{% endhighlight %}

(...)

Find and comment this line:

{% highlight apacheconf %}
# Include /private/etc/apache2/extra/httpd-vhosts.conf
{% endhighlight %}

add below:

{% highlight apacheconf %}
Include /private/etc/apache2/users/*.conf
{% endhighlight %}

Change permissions for virtual hosts storage directory (775):

{% highlight bash %}
sudo chmod -R 775 /private/etc/apache2/users
sudo chmod 775 /private/etc/apache2
{% endhighlight %}

Edit `hosts` file:

{% highlight bash %}
sudo vi /private/etc/hosts
{% endhighlight %}

Add host name redirection:

{% highlight text %}
127.0.0.1 ez1.lh
{% endhighlight %}

Start Apache 2 deamon:

{% highlight bash %}
sudo apachectl start
{% endhighlight %}

## 4. Install Composer globally: ##

{% highlight bash %}
curl -sS https://getcomposer.org/installer | php
mkdir -p /usr/local/bin
mv composer.phar /usr/local/bin/composer
{% endhighlight %}

## 5. Create a new database for eZ Platform: ##

Create new database (`ez1`):

{% highlight bash %}
/usr/local/mysql/bin/mysql -u root -e 'create database ez1;'
{% endhighlight %}

## 6. Install Brew package manager: ##

{% highlight bash %}
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
{% endhighlight %}

## 7. Install additional requirements for eZ Platform: ##

Install `PEAR/PECL` extension:

{% highlight bash %}
cd /usr/lib/php
sudo php install-pear-nozlib.phar
sudo pear channel-update pear.php.net
sudo pecl channel-update pecl.php.net
sudo pear upgrade-all
sudo pear config-set auto_discover 1
{% endhighlight %}

Install `autoconf`:

{% highlight bash %}
brew install autoconf
{% endhighlight %}

Install `intl`:

{% highlight bash %}
brew install icu4c
sudo pecl install intl
{% endhighlight %}

The path to the ICU libraries and headers is: `/usr/local/opt/icu4c/`.

Edit `/private/etc/php.ini` and add following line:
 
{% highlight ini %}
extension=intl.so
{% endhighlight %}

Enable `opcache` extension for PHP (suggested, but not required) by adding:

{% highlight ini %}
zend_extension=opcache.so
{% endhighlight %}

## 8. Install eZ Platform: ##

Go to the `~/Documents/workspace/ez1.lh` directory and set up directory permissions:

{% highlight bash %}
chmod 775 ../ez1.lh
chmod 775 ../../workspace
chmod 775 ../../../Documents
{% endhighlight %}

Clone eZ Platform repository:

{% highlight bash %}
git clone https://github.com/ezsystems/ezplatform.git .
{% endhighlight %}

Checkout latest stable version (eg. v1.0.1) or skip this step to use latest dev release from master branch. To see the list of all available tags type `git tag`.

{% highlight bash %}
git checkout v1.0.1
{% endhighlight %}

Copy virtual host template:

{% highlight bash %}
sudo cp doc/apache2/vhost.template /private/etc/apache2/users/ez1.lh.conf
{% endhighlight %}

Edit new virtual host:

{% highlight bash %}
sudo vi /private/etc/apache2/users/ez1.lh.conf
{% endhighlight %}

Modify virtual host file based on dev environment (or use template below):

*Replace `---USER_ID---` variable (used on line 10 and 17) with your current user ID. Use `whoami` command to get effective user ID of currently logged user. If you want to use default virtual host template (delivered with eZ Platform package) all you have to do is setup lines 7, 8, 9, 10, 17, 25 and 33.*

{% highlight apacheconf linenos %}
# Official VirtualHost configuration for Apache 2.x
# Note: This is meant to be tailored for your needs, expires headers might for instance not work for dev.
# Params: %IP_ADDRESS%, %PORT%, %HOST%, %HOST_ALIAS%, %BASEDIR%, %ENV% and %PROXY%

# NameVirtualHost %IP_ADDRESS%

<VirtualHost *:80>
    ServerName ez1.lh
    ServerAlias ez1.lh
    DocumentRoot "/Users/ ---USER_ID--- /Documents/workspace/ez1.lh/web"
    DirectoryIndex app.php

    # Enabled for Dev environment
    # LogLevel debug

    # "web" folder is what we expose to the world, all rewrite rules further down is relative to it.
    <Directory "/Users/ ---USER_ID--- /Documents/workspace/ez1.lh/web">
        # If using php configured in FastCGI mode, you might also need to add "ExecCGI" to the line below
        Options FollowSymLinks
        AllowOverride None
        # depending on your global Apache settings, you may need to uncomment and adapt:
        #  for Apache 2.2 and earlier:
        #Allow from all
        #  for Apache 2.4:
        Require all granted
    </Directory>

    ## eZ Platform ENVIRONMENT variables, used for customizing app.php execution (not used by console commands)

    # Environment.
    # Possible values: "prod" and "dev" out-of-the-box, other values possible with proper configuration
    # Defaults to "prod" if omitted (uses SetEnvIf so value can be used in rewrite rules)
    SetEnvIf Request_URI ".*" SYMFONY_ENV=dev

    # Whether to use custom ClassLoader (autoloader) file
    # Needs to be a valid path relative to root web/ directory
    # Defaults to bootstrap.php.cache, or autoload.php in debug
    #SetEnv SYMFONY_CLASSLOADER_FILE "../app/autoload.php"

    # Whether to use debugging.
    # Possible values: 0 or 1
    # Defaults to 0 if omitted, unless SYMFONY_ENV is set to: "dev"
    SetEnv SYMFONY_DEBUG %USE-DEBUGGING%

    # Whether to use Symfony's HTTP Caching.
    # Disable it if you are using an external reverse proxy (e.g. Varnish)
    # Possible values: 0 or 1
    # Defaults to 1 if omitted, unless SYMFONY_ENV is set to: "dev"
    #SetEnv SYMFONY_HTTP_CACHE 1

    # Whether to use custom HTTP Cache class if SYMFONY_HTTP_CACHE is enabled
    # Value must be a autoloadable cache class
    # Defaults to to use "AppCache"
    #SetEnv SYMFONY_HTTP_CACHE_CLASS "\Vendor\Project\MyCache"

    # Defines the proxies to trust.
    # Separate entries by a comma
    # Example: "proxy1.example.com,proxy2.example.org"
    # By default, no trusted proxies are set
    #SetEnv SYMFONY_TRUSTED_PROXIES "%PROXY%"

    <IfModule mod_rewrite.c>
        RewriteEngine On

        # For FastCGI mode or when using PHP-FPM, to get basic auth working.
        RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]

        # Needed for ci testing, you can optionally remove this.
        RewriteCond %{ENV:SYMFONY_ENV} "behat"
        RewriteCond %{REQUEST_URI} ^/php5-fcgi(.*)
        RewriteRule . - [L]

        # Cluster/streamed files rewrite rules. Enable on cluster with DFS as a binary data handler
        #RewriteRule ^/var/([^/]+/)?storage/images(-versioned)?/.* /app.php [L]

        RewriteRule ^/var/([^/]+/)?storage/images(-versioned)?/.* - [L]

        # Makes it possible to place your favicon at the root of your eZ Platform instance.
        # It will then be served directly.
        RewriteRule ^/favicon\.ico - [L]

        # Uncomment the line below if you want your favicon be served from the standard design.
        # You can customize the path to favicon.ico by bundle name and/or path.
        #RewriteRule ^/favicon\.ico /bundles/my-bundle/images/favicon.ico [L]

        # Give direct access to robots.txt for use by crawlers (Google, Bing, Spammers...)
        RewriteRule ^/robots\.txt - [L]

        # Platform for Privacy Preferences Project ( P3P ) related files for Internet Explorer
        # More info here : http://en.wikipedia.org/wiki/P3p
        RewriteRule ^/w3c/p3p\.xml - [L]

        # The following rule is needed to correctly display assets from eZ Platform / Symfony bundles
        RewriteRule ^/bundles/ - [L]

        # Additional Assetic rules for environments different from dev,
        # remember to run php app/console assetic:dump --env=prod
        RewriteCond %{ENV:SYMFONY_ENV} !^(dev)
        RewriteRule ^/(css|js|font)/.*\.(css|js|otf|eot|ttf|svg|woff) - [L]

        RewriteRule .* /app.php
    </IfModule>

    # Everything below is optional to improve performance by forcing
    # clients to cache image and design files, change the expires time
    # to suite project needs.
    <IfModule mod_expires.c>
        <LocationMatch "^/var/[^/]+/storage/images/.*">
            # eZ Platform appends the version number to image URL (ezimage
            # datatype) so when an image is updated, its URL changes too
            ExpiresActive on
            ExpiresDefault "now plus 10 years"
        </LocationMatch>
    </IfModule>
</VirtualHost>
{% endhighlight %}

Restart Apache 2 server:

{% highlight bash %}
sudo apachectl restart
{% endhighlight %}

Install required dependencies using Composer:

{% highlight bash %}
composer install
{% endhighlight %}

When Composer asks you for token you must login to your GitHub account and edit your profile. Go to the `Personal access tokens` link and `Generate new token` with default settings. Be aware that token will be shown only once, so do not refresh page until you paste token into Composer prompt. This operation is performed only once when you install eZ Platform for the first time.

Change directory permissions:

{% highlight bash %}
rm -rf app/cache/* app/logs/*
sudo chmod +a "_www allow delete,write,append,file_inherit,directory_inherit" app/{cache,logs,config} web
sudo chmod +a "`whoami` allow delete,write,append,file_inherit,directory_inherit" app/{cache,logs,config} web
{% endhighlight %}

Install eZ Platform:

{% highlight bash %}
php app/console ezplatform:install clean
{% endhighlight %}

If everything goes right, you should be able to see your page under <a href="http://ez1.lh" target="_blank">http://ez1.lh</a>. Please note that clean install of eZ Platform doesn't include `DemoBundle` anymore.

## 9. Optional: Install PHP 5.6 with opcache extension: ##

{% highlight bash %}
brew install -v homebrew/php/php56
chmod -R ug+w $(brew --prefix php56)/lib/php
brew install -v php56-opcache
{% endhighlight %}

Add proper `date.timezone` settings:

{% highlight bash %}
sudo vi /usr/local/etc/php/5.6/php.ini
{% endhighlight %}

Uncomment and modify:

{% highlight ini %}
date.timezone = "Europe/Warsaw"
{% endhighlight %}

(...)

Increase `memory_limit` value for eZ Platform:

{% highlight ini %}
memory_limit = 4G
{% endhighlight %}

(...)

Disable errors showing:

{% highlight ini %}
display_errors = Off
{% endhighlight %}

Change default PHP parser used by Apache:

{% highlight bash %}
sudo vi /private/etc/apache2/httpd.conf
{% endhighlight %}

Find and comment following line:

{% highlight apacheconf %}
# LoadModule php5_module libexec/apache2/libphp5.so
{% endhighlight %}

Add below:

{% highlight apacheconf %}
LoadModule php5_module /usr/local/opt/php56/libexec/apache2/libphp5.so
{% endhighlight %}

Install `intl` extension for PHP 5.6:

{% highlight bash %}
brew install php56-intl
{% endhighlight %}

Restart Apache:

{% highlight bash %}
sudo apachectl restart
{% endhighlight %}
