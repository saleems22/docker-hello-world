# docker
Testing out docker and docker compose

## Basic Docker

Docker Hub with PHP Apache images:
https://hub.docker.com/_/php/

### ```./Dockerfile```

```text
FROM php:7.0-apache
COPY src/ /var/www/html/
EXPOSE 80
```

### ```./src/index.php```

```php
<?php

echo "<h1>Hello, World</h1>";

?>
```

### Build Hello World docker image
To create the image <docker-hub-username>/hello-world, execute the following command on the jefftune/docker-hello-world folder:

```bash
$ docker login
$ docker build -t <docker-hub-username>/hello-world .
Sending build context to Docker daemon  97.28kB
Step 1/3 : FROM php:7.0-apache
 ---> 6619f3b4c19d
Step 2/3 : COPY src/ /var/www/html/
 ---> 63fcea499ba4
Removing intermediate container c2360d855f15
Step 3/3 : EXPOSE 80
 ---> Running in ce94b95f251a
 ---> 4b72e4266c68
Removing intermediate container ce94b95f251a
Successfully built 4b72e4266c68
Successfully tagged <docker-hub-username>/hello-world:latest
```

You can now push your new image to the registry:
```bash
$ sudo docker push <docker-hub-username>/hello-world
The push refers to a repository [docker.io/<docker-hub-username>/hello-world]
6763dbabe5aa: Pushed
c489531be3a1: Layer already exists
2c1d423ea400: Layer already exists
9a86dc3d1509: Layer already exists
1550ca974130: Layer already exists
5797b87f844d: Layer already exists
8108b96ed344: Layer already exists
acd74657641a: Layer already exists
753f5851a4ea: Layer already exists
98ac6c32b9bf: Layer already exists
8c31eae7fe91: Layer already exists
958c46160919: Layer already exists
c4066de46cb2: Layer already exists
0d960f1d4fba: Layer already exists
latest: digest: sha256:30c0a6f7ec2e91f404b465a5b8ca48e44f13ff8de3c2104ae998a42628add8ef size: 3242
```

### Running your Hello World docker image
Start your image and it will print container ID (example, 24f7baa2ae37xxxxxxx)

```bash
$ sudo docker run -d -p 80 -v /Users/<user>/github/jefftune/docker-hello-world/src/:/var/www/html/ <docker-hub-username>/hello-world
24f7baa2ae37xxxxxxx
```

Get the allocated external port:
```bash
$ sudo docker port 24f7baa2ae37xxxxxxx 80
0.0.0.0:32773
```

Test your deployment
```bash
$ curl 0.0.0.0:32773
<h1>Hello, World</h1>
```

## Notes:

https://www.youtube.com/watch?v=YFl2mCHdv24
https://hub.docker.com/_/php/

