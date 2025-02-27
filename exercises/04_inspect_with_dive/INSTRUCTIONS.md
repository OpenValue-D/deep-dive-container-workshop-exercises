# Description

This exercise shall demonstrate how to analyze container image layers with dive (see https://github.com/wagoodman/dive)

# Exercises

## Task 1

Analyze an open source image and get used to navigate in dive

* Run `dive postgres`
* Navigate in dive between different layers and see the corresponding command on the left
* Switch between layers and the file explorer on the right with <TAB>
* Filter the file explorer to show only changed files (CTRL-U)
* Try it out with an image of your choice

## Task 2

Use dive to find issues when building own images

* Check the Dockerfile to see that only the hello.sh is copied into the image
* Run `docker build -t dive-demo .`
* Check the build image with the standard command `docker history dive-demo`
* Check the layer size of the COPY command
* Run `dive dive-demo` to analyze the layer content of the COPY command
* Fix the Dockerfile (hint: check the content of the folder 04_inspect_with_dive in the terminal with `ls -la`)

## Task 3

Run dive in CI mode. Dive has a non-interactive CI mode usable to break a pipeline in case of inefficient image size

* Run dive with `CI=true dive dive-demo` to get direct outcome usable in pipelines

## Task 4 (optional)

Analyze and image of your own to find possible issues