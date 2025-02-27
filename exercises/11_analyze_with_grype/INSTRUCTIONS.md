# Description

This exercise shall demonstrate how to use grype to analyze the vulnerabilities of images

# Exercises

## Task 1

Analyze different images

* Run `grype my-distro` to see the packages
* Run `grype ubuntu:24.10` for comparison
* Choose an own image and run grype against it
* Finally run `grype mini-demo` to see vulnerabilities for ubuntu packages and java packages

## Task 2

Read in a sbom file instead of an image

* Generate a sbom file with `syft -o spdx-json ubuntu:24.10 > sbom.json`
* Run `grype sbom:./sbom.json`
* Download sbom attestation from previous exercise and run grype against it with `cosign download attestation ttl.sh/${MY_DISTRO}:1h | jq -r '.payload | @base64d | fromjson | .predicate' | grype --distro ubuntu:24.10`

## Task 3

Configure and filter grype output

* Run `grype postgres:17.2`
* Run `grype postgres:17.2 --ignore-states=wont-fix,not-fixed` to filter by states
* Run `grype postgres:17.2 --only-fixed` to have the same result
* Check that command run without failure with `echo $?` (should be 0)
* Configure another threshold to fail command with `grype postgres:17.2 --only-fixed -f critical` and see output
* Check that command run with failure with `echo $?` (should be 1 now)
* Generate file `.grype.yaml` with the following content

```yaml
ignore:
- fix-state: not-fixed
- fix-state: wont-fix
fail-on-severity: "Critical"
```

* Run `grype postgres:17.2`. Result should now be the same as `grype postgres:17.2 --only-fixed -f critical`
* See https://github.com/anchore/grype?tab=readme-ov-file#configuration for more configuration options

## Task 4

Get detailed informations about a vulnerability

* Run `grype postgres:17.2` and find out the CVE number of a critical vulnerability (e.g. CVE-2024-24790)
* Store the CVE number in a variable e.g. with `CVE=CVE-2024-24790`
* Run `grype postgres:17.2 -ojson | grype explain --id $CVE` to see detailed informations about the CVE
