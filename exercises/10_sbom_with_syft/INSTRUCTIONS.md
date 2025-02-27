# Description

This exercise shall demonstrate how to use syft to generate a sbom

# Exercises

## Task 1

Show sbom for different images

* Run `syft my-distro` to see the packages
* Run `syft ubuntu:24.10` for comparison
* Choose an own image and run syft against it
* Finally run `syft mini-demo` to see that syft also shows java packages and versions

## Task 2

Generate sbom files in different formats

* Run `syft -o FORMAT my-distro` with the different formats
* Save a sbom with `syft -o spdx-json ubuntu:24.10 > sbom.json` 
* Check the content with `jq '.' sbom.json`
* Check the found license information of the packages with `jq '.packages[].licenseDeclared' sbom.json`

## Task 3

Link sbom to image as attestation

* Run `cosign generate-key-pair` with empty password to have a new key pair for the attestation
* Upload my-distro to ttl.sh. First run `MY_DISTRO=$(uuidgen | tr '[:upper:]' '[:lower:]')`, then `docker tag my-distro ttl.sh/${MY_DISTRO}:4h`
* Push image with `docker push ttl.sh/${MY_DISTRO}:4h`
* Run `syft attest --key cosign.key -o spdx-json ttl.sh/${MY_DISTRO}:4h > my_distro_sbom_attestation.json`
* Check the output of the command. The sbom is uploaded as image artifact to the registry alongside the real image
* Verify sbom with `cosign verify-attestation --key cosign.pub --type spdxjson ttl.sh/${MY_DISTRO}:4h | jq '.payload | @base64d | fromjson | .predicate'`
* Check output of the command
* Download the sbom `cosign download attestation ttl.sh/${MY_DISTRO}:4h | jq -r '.payload | @base64d | fromjson | .predicate' > sbom.json`
* Check the content of `sbom.json`

## Task 4

Generate sbom for local project. Syft can generate sboms also based on pom.xml, but also with direct dependencies

* Run `syft ../08_own_jre` (see quite short list of direct dependencies)