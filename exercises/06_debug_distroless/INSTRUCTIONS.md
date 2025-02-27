# Description

This exercise shall demonstrate how to debug distroless applications locally without rebuilding the image

# Exercises

## Task 1

Use docker-debug to check a running distroless container

* Run `docker build -t debug-demo .`
* Run `docker run --rm --name debug-demo -d -p 3000:8080 debug-demo`
* Open `http://localhost:3000` in the browser to see it work
* Try to open a shell in the container with `docker exec debug-demo sh` to see it fail
* Run `docker-debug debug-demo bash` to open a debug session for the running container
* Run `ps fax` to see that the debug session is running in the container
* Run `cat /mnt/container/usr/share/nginx/html/index.html` to see that the debug session has access to running container's filesystem
* Change the index.html in the container with vi to see immediate result on `http://localhost:3000`
* Run `exit` to leave the debug session

## Task 2

Use nixery for adhoc debug images (see https://nixery.dev)

* Nixery has the ability to build images on the fly based on nix packages. Packages are part of the image name and can be freely combined
* Run `docker-debug -i nixery.dev/shell/htop debug-demo sh`
* Run `htop` to see the packages installed
* Exit the debug session and try a different image (see https://search.nixos.org/packages for possible packages)