# Description

This exercise shall demonstrate how to use cosign to sign images and to verify the signature

# Exercises

## Task 1

Sign image with private key

* Run `cosign generate-key-pair` with empty password to have a new key pair for the attestation
* Run `SIGN_DEMO=$(uuidgen | tr '[:upper:]' '[:lower:]')` and build image with `docker build -t ttl.sh/${SIGN_DEMO}:4h .`
* Push image `docker push ttl.sh/${SIGN_DEMO}:4h`
* Run `cosign sign --key cosign.key -y ttl.sh/${SIGN_DEMO}:4h` to sign image with local key.
* Run `cosign verify --key cosign.pub ttl.sh/${SIGN_DEMO}:4h` to verify signature
* Verify output checks

## Task 2

Sign image by digest (recommended)

* Extract image digest with `IMAGE_DIGEST=$(docker inspect ttl.sh/${SIGN_DEMO}:4h | jq -r '.[] | .RepoDigests[0]')`
* Run `echo ${IMAGE_DIGEST}` to see digest
* Run `cosign sign --key cosign.key -y ${IMAGE_DIGEST}` to sign image with local key.
* Run `cosign verify --key cosign.pub ${IMAGE_DIGEST}` to verify signature
* Verify output checks

## Task 3

Download signature. The signature can be downloaded to e.g. be verified by other tools

* Run `cosign download signature ${IMAGE_DIGEST} | jq '.'` to download signature and pretty print it