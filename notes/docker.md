### Download image

```bash
docker pull %image_name%:%tag%
```

### List downloaded images

```bash
docker images
```

### List commands that build image (Dockerfile content)

```bash
docker history %image_name%:%tag%
```

### Delete image

```bash
docker rmi %image_name%:%tag%
```

### Delete all images

```bash
docker rmi $(docker images -q)
```

### Run container under custom name

```bash
docker run --name="%shortname%" %image_name%:%tag%
```

### Run container in background mode (deamon)

```bash
docker run -d %image_name%:%tag%
```

### Run specific command inside container (and exit after completed)

```bash
docker run --rm=true %image_name%:%tag%
```

### List all containers

```bash
docker ps -a
```

### Stop container

```bash
docker stop %name%
```

### Delete container

```bash
docker rm %name%
```

### Delete all containers

```bash
docker rm $(docker ps -a -q)
```

### Overwrite built-in container command

```bash
docker run %name% %command%
```

### Run command on already working container

```bash
docker exec %name% %command%
```

### Attach to already working container (CTRL+C - quit)

```bash
docker attach %name%
```

### Attach to container and leave it while still working

```bash
docker run -t --name=%container_name% %image_name%
docker attach %container_name%
# Ctrl+C
```

or 

```bash
docker run -ti --name=%container_name% %image_name%
docker attach %container_name%
# Ctrl+P Ctrl+Q
```

or

```bash
docker run --name=%container_name% %image_name%
docker attach --sig-term=false %container_name%
# Ctrl+C
```

### Browse file system inside container

```bash
docker exec -it %container_name% bash
```

### Redirect container ports

```bash
docker run -d -p 9000:5432 %image_name%:%tag%
```

In this example internal port 5432 is redirected to port 9000 which is accessible from the host computer.

### Link containers using ports

```bash
docker run -d --expose=5432 --name="%shortname1%" %image_name1%
docker run -d -it --name="shortname2" --link="%shortname1%" %image_name2%
```

### Mount host file system

```bash
docker run -v %host_path%:%container_path% %image_name%
```

### Serve files using Python inside docker container

```bash
docker run -d -v ~/docker:/shared_volume -p 8000:8000 python:3.5-slim /bin/bash -c "cd /shared_volume && python -m http.server 8000"
```

Files should be available under http://127.0.0.1:8000/ path.

### Link files between containers

```bash
docker create -v %container_inside_path% --name %container_name1% %image_name1%
docker run --volumes-from %container_name1% %image_name2%
```

Note: you don't have to run container to get access to it's file system.

### Set environment variable during docker run

```bash
docker run -e %name%:%value% %image_name%
```

### Display container logs

```bash
docker logs %container_name%
```

### Setup Wordpress together with MariaDB

```bash
docker pull mariadb
docker pull wordpress

docker run -d --name=maria -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wp -e MYSQL_PASSWORD=root mariadb
docker run -d --name=word --link=maria:mysql -p 8080:80 wordpress
```

Working instance should be available under http://127.0.0.1:8080
