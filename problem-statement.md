You are given a Dockerfile (https://gist.github.com/prmishra/0ae5b40bff67bbad4a887f4b4052835d) which produces approximately 650MB size docker image. Your task is to optimize this Dockerfile to reduce size of the resultant docker image without changing behaviour of the application.

You should use multi-stage build and alpine image. Ensure that you are able to create an image using the optimized Dockerfile before submitting. Ideally the resultant docker image should be less than 10mb in size.

Copy and paste optimized Dockerfile into the textbox. Your submission will be automatically evaluated. So ensure that you run your code before submitting

https://docs.docker.com/develop/develop-images/multistage-build/
https://blog.alexellis.io/mutli-stage-docker-builds/


docker build -t hrmnjt/sample-go-image:latest -f Dockerfile
