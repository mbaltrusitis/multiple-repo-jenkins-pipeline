# multiple-repo-jenkins-pipeline

The objective is to have this `master` repo's Jenkinsfile checkout two other repositories without an error. In this example we are using Requests and Pelican. *Do not say to just use pip.* These are just example repositories I am using for this exercise.

The current state of `Jenkinsfile` produces the following behavior:

✅ Pipeline creates subdirectories for build deps.
✅ Pipeline properly checks-out the root repo (this one)
✅ Pipeline properly checks-out repo A (Python's Requests)
❗️Pipeline fails to check-out repo B (Python’s Pelican)

The error message for the second sibling repo:

```text

```
