# Description

This exercise shall demonstrate how to build your own distroless image based on ubuntu and chisel.

# Exercises

## Task 1

Create a distroless image with chisel

* Check the Dockerfile to see the how chisel is used
* Run `docker build -t my-distro .`
* Check image content with `dive my-distro`
* Try to run `docker run --rm -it my-distro sh` to see it fail

## Task 2

Add additional packages to distroless (e.g. a bash)

* Extend the Dockerfile in line 21 with `bash_bins` to install the binaries for bash
* Rebuild the image
* Check image content with `dive my-distro`
* Try `docker run --rm -it my-distro bash` to see it work now
* Try to add other slices (see https://github.com/canonical/chisel-releases/tree/ubuntu-24.10/slices)