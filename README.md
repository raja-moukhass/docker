# docker
you’re thinking with containers... Row, row, row your boat... gently down the stream...

## Get Docker
Estimated reading time: 1 minute
Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.

You can download and install Docker on multiple platforms. Refer to the following section and choose the best installation path for you.
### Installation 
Docker is available in two editions: Community Edition (CE) and Enterprise Edition (EE).

Docker Community Edition (CE) is ideal for developers and small teams looking to get started with Docker and experimenting with container-based apps. Docker CE has two update channels, stable and edge:

- Stable gives you reliable updates every quarter
- Edge gives you new features every month
- For more information about Docker CE, see Docker Community Edition.

Docker Enterprise Edition (EE) is designed for enterprise development and IT teams who build, ship, and run business critical applications in production at scale. For more information about Docker EE, including purchasing options, see Docker Enterprise Edition.

The basic docker run command takes this form:

```sh
$  docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]
```

this command attempts to start the nginx service
```sh
$  docker run -d -p 80:80 my_image service nginx start
```
Create this Dockerfile
```sh
$ FROM alpine:latest
$ RUN apk add --update htop && rm -rf /var/cache/apk/*
$ CMD ["htop"]
```
Build the Dockerfile and tag the image as myhtop:
```sh
$ docker build -t myhtop .
```
Use the following command to run htop inside a container
```sh
$ docker run -it --rm --pid=host myhtop
```
### sources
- <a href="https://docs.docker.com/engine/reference/run/">there is nothing better than docker documentation</a>
