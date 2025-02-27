# Description

This exercise shall demonstrate the difference between the shell and exec format for CMD or ENTRYPOINT.

# Exercises

## Task 1

Build a web application and run it in shell format

* Open main.go to see line 36 (prints a received SIGTERM)
* Open the Dockerfile (see CMD in shell format)
* Build the image with `docker build -t shell-demo .`
* Run the image with `docker run -d --name shell-demo shell-demo` and check the status with `docker ps`
* Check the main process (PID 1) of the container with `docker exec shell-demo ps fax` (should be /bin/sh)
* Stop the container and measure the time with `time docker stop shell-demo` (should take ~10s as the default timeout of docker before sending a kill command)
* Check that the go app did not receive a SIGTERM by checking the logs with `docker logs shell-demo`
* Check that the container processed was killed (Status code 137) with `docker inspect shell-demo | jq '.[] | .State.ExitCode'`
* Remove container with `docker rm shell-demo`

## Task 2

Demonstrates the effect of the exec format

* Change the CMD in the Dockerfile to exec format (`CMD ["/app"]`)
* Build the image iwth `docker build -t exec-demo .`
* Run the image with `docker run -d --name exec-demo exec-demo` and check the status with `docker ps`
* Check the main process (PID 1) of the container with `docker exec exec-demo ps fax` (should be /app)
* Stop the container and measure the time with `time docker stop exec-demo` (should take <1s as the app handles the SIGTERM)
* Check that the go app did receive a SIGTERM by checking the logs with `docker logs exec-demo`
* Check that the container stopped gracefully with `docker inspect exec-demo | jq '.[] | .State.ExitCode'`
* Remove container with `docker rm exec-demo`