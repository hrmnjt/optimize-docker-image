# Optimize the docker image by using multi-stage builds

Original Dockerfile (./Dockerfile.original) which produces approximately 690MB size docker image. To optimize this Dockerfile for reducing footprint for resultant docker image without changing behaviour of the application.

Idea is to multi-stage build and alpine image (can be done using a scratch:latest image as well). Best case scenario would be to have resultant docker image 10mb in size.

For reference please read the blogs and official documentation:
* https://docs.docker.com/develop/develop-images/multistage-build/
* https://blog.alexellis.io/mutli-stage-docker-builds/

## Usage

Running the original dockerfile to create the docker image for base Golang 1.7.3 
```sh
docker build -t original-image:latest -f Dockerfile.original .
docker run --name original-app -it original-image
```
Checking the size of the docker images
```sh
docker images
# REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
# original-image      latest              fe646450aee1        41 seconds ago      693MB
# golang              1.7.3               ef15416724f6        2 years ago         672MB
```

Running the optimized dockerfile which improves:
* Using a alpine image on second stage
* Stripping off most element from the layers which are not needed (in our `app.go` example there is no need to add ca-certificates and hence the step has been commented. Please uncomment in case any request is made in the application)


```sh
docker build -t optimized-image:latest -f Dockerfile.optimized .
docker run --name optimized-app -it optimized-image
```

Checking the size of the docker images
```sh
docker images
# REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
# optimized-image     latest              e7032d807151        2 seconds ago       7.16MB
# original-image      latest              fe646450aee1        41 seconds ago      693MB
# alpine              latest              caf27325b298        3 weeks ago         5.53MB
# golang              1.7.3               ef15416724f6        2 years ago         672MB
```
Docker image had come down from **693MB to 7.16MB** which is a great way of creating images without loosing any functionality.
