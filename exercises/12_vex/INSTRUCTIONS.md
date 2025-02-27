# Description

This exercise shall demonstrate how to use vexctl to generate vex documents to filter out false-positives.

# Exercises

## Task 1

Generate a vex document

* Run `grype alpine:3.17.10` and take the first CVE id `CVE-2024-9143`
* Generate a new vex document with `vexctl create -j "vulnerable_code_not_in_execute_path" "pkg:oci/alpine?tag=3.17.10" CVE-2024-9143 not_affected --file CVE-2024-9143.vex.json`
* Check the resulting document with `jq '.' CVE-2024-9143.vex.json`

## Task 2

Merge two vex documents

* Generate a second vex document for the second CVE `CVE-2024-13176` with the name CVE-2024-13176.vex.json
* Use a valid justification and status (see `vexctl list justification` and `vexctl list status` for valid values)
* e.g. `vexctl create "pkg:oci/alpine?tag=3.17.10" CVE-2024-13176 fixed --file CVE-2024-13176.vex.json`
* Merge both documents with `vexctl merge CVE-2024-9143.vex.json CVE-2024-13176.vex.json > alpine.vex.json`
* Check the resulting document with `jq '.' alpine.vex.json`

## Task 3

Use the vex document to filter content from vulnerability scanners

* Generate file `.grype.yaml` with the following content

```yaml
ignore:
- vex-status: not_affected
- vex-status: fixed
```
* Run `grype --vex CVE-2024-9143.vex.json alpine:3.17.10` to see how one CVE gets suppressed based on the vex document
* Run `grype --vex CVE-2024-13176.vex.json alpine:3.17.10` to see how the other CVE gets suppressed based on the vex document
* Run `grype --vex alpine.vex.json alpine:3.17.10` to see how all CVEs get suppressed based on the vex document
* Run `grype --vex alpine.vex.json --show-suppressed alpine:3.17.10` to show suppressed CVEs in the list again

## Task 4

Attach a vex document to an image as attestation

* Run `cosign generate-key-pair` with empty password to have a new key pair for the attestation
* Run `VEX_DEMO=$(uuidgen | tr '[:upper:]' '[:lower:]')` to generate name for usage with ttl.sh
* Tag image and push it to ttl.sh with `docker tag alpine:3.17.10 ttl.sh/${VEX_DEMO}:8h && docker push ttl.sh/${VEX_DEMO}:8h`
* Run `cosign attest --predicate alpine.vex.json --type openvex --key cosign.key ttl.sh/${VEX_DEMO}:8h` to attach the vex document to the image
* Verify vex with `cosign verify-attestation --type openvex --key cosign.pub ttl.sh/${VEX_DEMO}:8h | jq '.payload | @base64d | fromjson | .predicate'`