# Description

This exercise shall demonstrate how to use distroless images as base for own applications

# Exercises

## Task 1

Minimize own image with distroless

* Run `docker build -t distroless-demo .`
* Run `docker run distroless-demo` to see that it works
* Run `docker image ls | grep distroless` to see the size of the image (quite big for only a hello world)
* Run `docker run --rm -it distroless-demo bash` to see that a shell is included (Run `exit` to get back)
* Change FROM in Dockerfile to `FROM cgr.dev/chainguard/static` and rebuild the image
* Rerun `docker run distroless-demo` and `docker image ls | grep distroless` to see the new result
* Try to open a shell in the container with `docker run --rm -it distroless-demo bash` and see it fail
* Change FROM in Dockerfile to `FROM scratch` and rebuild the image
* Check size and if it is runnable to see that static binaries do not need any libraries in the image

## Task 2

Analyze different distroless images

* Check different distroless images with dive to see the different content (e.g. `dive cgr.dev/chainguard/static` and `dive cgr.dev/chainguard/cc-dynamic`)
* See other distroless images (https://images.chainguard.dev/) usable for different languages (e.g. `cgr.dev/chainguard/aspnet-runtime` and `cgr.dev/chainguard/jre`)