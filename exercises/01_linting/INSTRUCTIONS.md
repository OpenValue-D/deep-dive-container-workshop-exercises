# Description

This exercise shall demonstrate the usage of hadolint as a Dockerfile linter. It shows how hadolint is used and how it can be configured

# Exercises

## Task 1

Use hadolint to find issues.

* Open the terminal in VSCode
* Run `hadolint Dockerfile`
* Check the result
* Visit https://github.com/hadolint/hadolint?tab=readme-ov-file#rules to get more details for each issue and how to fix it
* Fix DL3027 with the help of the rule documentation (https://github.com/hadolint/hadolint/wiki/DL3027)
* Rerun hadolint and see a new issue in line 9
* Fix the new issue in line 9 (use version `2:1.22~2build1` for the golang-go package)

## Task 2

Configure hadolint to ignore specific issues.

* Add `# hadolint ignore=DL3059` in line 9 of the Dockerfile
* Rerun hadolint to see the result
* Check command result status with `echo $?` (shows 1 as failure)
* Add `# hadolint global ignore=DL3020` in line 1 of the Dockerfile to ignore all occurences of an issue
* Rerun hadolint to see the result

## Task 3

Use hadolint to check for necessary labels.

* Run hadolint with `hadolint --require-label maintainer:text Dockerfile`
* Check the result with a new info for missing label
* Add the label in the Dockerfile and rerun the command
* Run hadolint with `hadolint --strict-labels Dockerfile`
* Check the result with a new info for unnecessary labels
* Remove the unnecessary label and rerun the command

## Task 4

Configure hadolint via configuration file.

* Create a file called .hadolint.yaml
* Add the following content to the file

```yaml
ignored:
- DL3025
override:
  error:
  - DL3009
no-fail: true
```

* Rerun hadolint to see the result
* Check that the command result does not fail anymore with `echo $?`
* Check https://github.com/hadolint/hadolint?tab=readme-ov-file#configure for more configuration options

## Task 5

See integration in action to get linting directly in the editor

* Go to the extensions in VSCode
* Install the hadolint extension (identifier = exiasr.hadolint)
* Open the Dockerfile in VSCode and see the hadolint results in line
* Fix all issues