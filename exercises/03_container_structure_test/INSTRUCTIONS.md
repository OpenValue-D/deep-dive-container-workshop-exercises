# Description

This exercise shall demonstrate how to write structure tests for container images (see https://github.com/GoogleContainerTools/container-structure-test)

# Exercises

## Task 1

Build a web application and run structure tests

* Build the image with `docker build -t test-demo .`
* Check the tests.yaml for predefined tests
* Run the tests against the image with `container-structure-test test -i test-demo -c tests.yaml`
* Fix the image to make the tests pass (hint: see https://hub.docker.com/_/node to find the right image tag)
* Rebuild the image and rerun the tests

## Task 2

Create a test to check non-existence of a file

* The current Dockerfile copies not only the app.mjs into the image, but also the Dockerfile and tests.yaml
* Extend the tests to check that the files `/app/Dockerfile` and `/app/tests.yaml` do not exist (see https://github.com/GoogleContainerTools/container-structure-test?tab=readme-ov-file#file-existence-tests)
* Rerun the tests to see the new tests fail
* Fix the image to make the tests pass
* Rebuild the image and rerun the tests

## Task 3

Create a test to check the content of a file

* We want to check that the image is based on alpine
* Extend the tests to check for the content of the file `/etc/os-release` to contain `.*alpine.*` (see https://github.com/GoogleContainerTools/container-structure-test?tab=readme-ov-file#file-content-tests)
* Rerun the tests to see the new test fail
* Fix the image to make the tests pass (hint: see https://hub.docker.com/_/node to find the right image tag)
* Rebuild the image and rerun the tests
