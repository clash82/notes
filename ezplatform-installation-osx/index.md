---
layout: default
title: eZ Publish / eZ Platform (MacOS X clean install)
---

This guide allows you to prepare environment required to install eZ Publish / Platform on MacOS X Yosemite.

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

Increase `memory_limit` value for eZ Publish / Platform:

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

## 5. Create a new database for eZ Publish / Platform: ##

Create new database (`ez1`):

{% highlight bash %}
/usr/local/mysql/bin/mysql -u root -e 'create database ez1;'
{% endhighlight %}

## 6. Install Brew package manager: ##

{% highlight bash %}
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
{% endhighlight %}

## 7. Install additional requirements for eZ Publish / Platform: ##

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

## 8. Install eZ Publish / eZ Platform: ##

Go to the `~/Documents/workspace/ez1.lh` directory and set up directory permissions:

{% highlight bash %}
chmod 775 ../ez1.lh
chmod 775 ../../workspace
chmod 775 ../../../Documents
{% endhighlight %}

Clone eZ Publish / Platform repository:

{% highlight bash %}
git clone https://github.com/ezsystems/ezplatform.git .
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

*Replace `---USER_ID---` variable (used on line 5 and 8) with current user ID. Use `whoami` command to get effective user ID of currently logged user. If you want to use default virtual host template (delivered with eZ Publish/Platform package) all you have to do is setup lines 1, 2, 3, 5, 8 and 17.*

{% highlight apacheconf linenos %}
<VirtualHost *:80>
    ServerName ez1.lh
    ServerAlias ez1.lh

    DocumentRoot "/Users/ ---USER_ID--- /Documents/workspace/ez1.lh/web"
    DirectoryIndex index.php

    <Directory "/Users/ ---USER_ID--- /Documents/workspace/ez1.lh/web">
        Options FollowSymLinks
        AllowOverride None
        Require all granted
    </Directory>

    # Environment.
    # Possible values: "prod" and "dev" out-of-the-box, other values possible with proper configuration
    # Defaults to "prod" if omitted (uses SetEnvIf so value can be used in rewrite rules)
    SetEnvIf Request_URI ".*" ENVIRONMENT=dev

    # Whether to use Symfony's ApcClassLoader.
    # Possible values: 0 or 1
    # Defaults to 0 if omitted, supported on 5.2 and higher
    #SetEnv USE_APC_CLASSLOADER 0

    # Prefix used when USE_APC_CLASSLOADER is set to 1.
    # Use a unique prefix in order to prevent cache key conflicts
    # with other applications also using APC.
    # Defaults to "ezpublish" if omitted, supported on 5.2 and higher
    #SetEnv APC_CLASSLOADER_PREFIX "ezpublish"

    # Whether to use debugging.
    # Possible values: 0 or 1
    # Defaults to 0 if omitted, unless ENVIRONMENT is set to: "dev", supported on 5.2 and higher
    #SetEnv USE_DEBUGGING 0

    # Whether to use Symfony's HTTP Caching.
    # Disable it if you are using an external reverse proxy (e.g. Varnish)
    # Possible values: 0 or 1
    # Defaults to 1 if omitted, unless ENVIRONMENT is set to: "dev", supported on 5.2 and higher
    #SetEnv USE_HTTP_CACHE 1

    # Defines the proxies to trust.
    # Separate entries by a comma
    # Example: "proxy1.example.com,proxy2.example.org"
    # By default, no trusted proxies are set, supported on 5.2 and higher
    #SetEnv TRUSTED_PROXIES "%PROXY%"

    <IfModule mod_rewrite.c>
        RewriteEngine On

        # Uncomment in FastCGI mode or when using PHP-FPM, to get basic auth working.
        RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]

        # Needed for ci testing, remove in prod.
        RewriteCond %{ENV:ENVIRONMENT} "behat"
        RewriteCond %{REQUEST_URI} ^/php5-fcgi(.*)
        RewriteRule . - [L]

        # v1 rest API is on Legacy
        RewriteRule ^/api/[^/]+/v1/ /index_rest.php [L]

        # If using cluster, uncomment the following two lines:
        ## For 5.4 and higher:
        #RewriteRule ^/var/([^/]+/)?storage/images(-versioned)?/.* /index.php [L]
        #RewriteRule ^/var/([^/]+/)?cache/(texttoimage|public)/.* /index_cluster.php [L]
        ## Versions prior to 5.4:
        #RewriteRule ^/var/([^/]+/)?storage/images(-versioned)?/.* /index_cluster.php [L]
        #RewriteRule ^/var/([^/]+/)?cache/(texttoimage|public)/.* /index_cluster.php [L]

        RewriteRule ^/var/([^/]+/)?storage/images(-versioned)?/.* - [L]
        RewriteRule ^/var/([^/]+/)?cache/(texttoimage|public)/.* - [L]
        RewriteRule ^/design/[^/]+/(stylesheets|images|javascript|fonts)/.* - [L]
        RewriteRule ^/share/icons/.* - [L]
        RewriteRule ^/extension/[^/]+/design/[^/]+/(stylesheets|flash|images|lib|javascripts?)/.* - [L]
        RewriteRule ^/packages/styles/.+/(stylesheets|images|javascript)/[^/]+/.* - [L]
        RewriteRule ^/packages/styles/.+/thumbnail/.* - [L]
        RewriteRule ^/var/storage/packages/.* - [L]

        # Makes it possible to place your favicon at the root of your
        # eZ Publish instance. It will then be served directly.
        RewriteRule ^/favicon\.ico - [L]

        # Uncomment the line below if you want your favicon be served
        # from the standard design. You can customize the path to
        # favicon.ico by changing /design/standard/images/favicon\.ico
        #RewriteRule ^/favicon\.ico /design/standard/images/favicon.ico [L]
        RewriteRule ^/design/standard/images/favicon\.ico - [L]

        # Give direct access to robots.txt for use by crawlers (Google,
        # Bing, Spammers..)
        RewriteRule ^/robots\.txt - [L]

        # Platform for Privacy Preferences Project ( P3P ) related files
        # for Internet Explorer
        # More info here : http://en.wikipedia.org/wiki/P3p
        RewriteRule ^/w3c/p3p\.xml - [L]

        # Uncomment the following lines when using popup style debug in legacy
        #RewriteRule ^/var/([^/]+/)?cache/debug\.html.* - [L]

        # Following rule is needed to correctly display assets from eZ Publish5 / Symfony bundles
        RewriteRule ^/bundles/ - [L]

        # Additional Assetic rules for prod env, remember to run php ezpublish/console assetic:dump --env=prod
        RewriteCond %{ENV:ENVIRONMENT} "prod"
        RewriteRule ^/(css|js)/.*\.(css|js) - [L]

        # Conditions for enabling webdav and soap interfaces from legacy
        ## Symlink files into your web folder and correct domain names to be valid server aliases
        #RewriteCond %{HTTP_HOST} ^webdav\..*
        #RewriteRule ^(.*) /webdav.php [L]
        #RewriteCond %{HTTP_HOST} ^soap\..*
        #RewriteRule ^(.*) /soap.php [L]

        # For 5.x versions prior to 5.2, enable this to use dev env based on ENVIRONMENT variable set above
        #RewriteCond %{ENV:ENVIRONMENT} "dev"
        #RewriteRule .* /index_dev.php [L]

        RewriteRule .* /index.php
    </IfModule>

    # Everything below is optional to improve performance by forcing
    # clients to cache image and design files, change the expires time
    # to suite project needs.
    <IfModule mod_expires.c>
        <LocationMatch "^/var/[^/]+/storage/images/.*">
            # eZ Publish appends the version number to image URL (ezimage
            # datatype) so when an image is updated, its URL changes to
            ExpiresActive on
            ExpiresDefault "now plus 10 years"
        </LocationMatch>

        <LocationMatch "^/extension/[^/]+/design/[^/]+/(stylesheets|images|javascripts?|flash)/.*">
            # A good optimization if you don't change your design often
            ExpiresActive on
            ExpiresDefault "now plus 5 days"
        </LocationMatch>

        <LocationMatch "^/extension/[^/]+/design/[^/]+/lib/.*">
            # Libraries get a new url (version number) on updates
            ExpiresActive on
            ExpiresDefault "now plus 90 days"
        </LocationMatch>

        <LocationMatch "^/design/[^/]+/(stylesheets|images|javascripts?|lib|flash)/.*">
            # Same as above for bundled eZ Publish designs
            ExpiresActive on
            ExpiresDefault "now plus 7 days"
        </LocationMatch>

        <LocationMatch "^/share/icons/.*">
            # Icons as used by admin interface, barly change
            ExpiresActive on
            ExpiresDefault "now plus 7 days"
        </LocationMatch>

        # When ezjscore.ini/[Packer]/AppendLastModifiedTime=enabled
        # so that file names change when source files are modified
        #<LocationMatch "^/var/[^/]+/cache/public/.*">
            # Force ezjscore packer js/css files to be cached 30 days
            # at client side
            #ExpiresActive on
            #ExpiresDefault "now plus 30 days"
        #</LocationMatch>
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

When Composer asks you for token you must login to your GitHub account and edit your profile. Go to the `Personal access tokens` link and `Generate new token` with default settings. Be aware that token will be shown only once, so do not refresh page until you paste token into Composer prompt. This operation is performed only once when you install eZ Publish/Platform for the first time.

Change directory permissions:

{% highlight bash %}
rm -rf ezpublish/cache/* ezpublish/logs/* ezpublish/sessions/*
sudo chmod +a "_www allow delete,write,append,file_inherit,directory_inherit" ezpublish/{cache,logs,config,sessions} web
sudo chmod +a "`whoami` allow delete,write,append,file_inherit,directory_inherit" ezpublish/{cache,logs,config,sessions} web
{% endhighlight %}

Install eZ Publish / Platform:

{% highlight bash %}
php ezpublish/console ezplatform:install demo
{% endhighlight %}

If everything goes right, you should see your page under <a href="http://ez1.lh" target="_blank">http://ez1.lh</a>.

## 9. Optional: Install PHP 5.6 with opcache: ##

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

Increase `memory_limit` value for eZ Publish / Platform:

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
