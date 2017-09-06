---
layout: default
title: Docker
---

## Download image: ##

{% highlight bash %}
docker pull %image_name%:%tag%
{% endhighlight %}

## List downloaded images: ##

{% highlight bash %}
docker images
{% endhighlight %}

## List commands that build image (dockerfile content): ##

{% highlight bash %}
docker history %image_name%:%tag%
{% endhighlight %}

## Delete image: ##

{% highlight bash %}
docker rmi %image_name%:%tag%
{% endhighlight %}

## Delete all images: ##

{% highlight bash %}
docker rmi $(docker images -q)
{% endhighlight %}

## Run container under custom name: ##

{% highlight bash %}
docker run --name="%shortname%" %image_name%:%tag%
{% endhighlight %}

## Run container in background mode (deamon): ##

{% highlight bash %}
docker run -d %image_name%:%tag%
{% endhighlight %}

## Run specific command inside container (and exit after completed): ##

{% highlight bash %}
docker run --rm=true %image_name%:%tag%
{% endhighlight %}

## List all containers: ##

{% highlight bash %}
docker ps -a
{% endhighlight %}

## Stop container: ##

{% highlight bash %}
docker stop %name%
{% endhighlight %}

## Delete container: ##

{% highlight bash %}
docker rm %name%
{% endhighlight %}

## Delete all containers: ##

{% highlight bash %}
docker rm $(docker ps -a -q)
{% endhighlight %}

## Overwrite built-in container command: ##

{% highlight bash %}
docker run %name% %command%
{% endhighlight %}

## Run command on already working container: ##

{% highlight bash %}
docker exec %name% %command%
{% endhighlight %}

## Attach to already working container (CTRL+C - quit): ##

{% highlight bash %}
docker attach %name%
{% endhighlight %}

## Attach to container and leave it while still working: ##

{% highlight bash %}
docker run -t --name=%container_name% %image_name%
docker attach %container_name%
Ctrl+C
{% endhighlight %}

or 

{% highlight bash %}
docker run -ti --name=%container_name% %image_name%
docker attach %container_name%
Ctrl+P Ctrl+Q
{% endhighlight %}

or

{% highlight bash %}
docker run --name=%container_name% %image_name%
docker attach --sig-term=false %container_name%
Ctrl+C
{% endhighlight %}

## Browse file system inside container: ##

{% highlight bash %}
docker exec -it %container_name% bash
{% endhighlight %}

## Redirect container ports: ##

{% highlight bash %}
docker run -d -p 9000:5432 %image_name%:%tag%
{% endhighlight %}

In this example internal port 5432 is redirected to port 9000 which is accessible from the host computer.

## Link containers using ports: ##

{% highlight bash %}
docker run -d --expose=5432 --name="%shortname1%" %image_name1%
docker run -d -it --name="shortname2" --link="%shortname1%" %image_name2%
{% endhighlight %}

## Mount host file system: ##

{% highlight bash %}
docker run -v %host_path%:%container_path% %image_name%
{% endhighlight %}

## Serve files using Python inside docker container: ##

{% highlight bash %}
docker run -d -v ~/docker:/shared_volume -p 8000:8000 python:3.5-slim /bin/bash -c "cd /shared_volume && python -m http.server 8000"
{% endhighlight %}

Files should be now accessible under http://127.0.0.1:8000/ path.

## Link files between containers: ##

{% highlight bash %}
docker create -v %container_inside_path% --name %container_name1% %image_name1%
docker run --volumes-from %container_name1% %image_name2%
{% endhighlight %}

Note: you don't have to run container to get access to it's file system.

## Set environment variable during docker run: ##

{% highlight bash %}
docker run -e %name%:%value% %image_name%
{% endhighlight %}

## Display container logs: ##

{% highlight bash %}
docker logs %container_name%
{% endhighlight %}

## Setup Wordpress together with MariaDB: ##

{% highlight bash %}
docker pull mariadb
docker pull wordpress

docker run -d --name=maria -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wp -e MYSQL_PASSWORD=root mariadb
docker run -d --name=word --link=maria:mysql -p 8080:80 wordpress
{% endhighlight %}

Working instance should be accessible under http://127.0.0.1:8080