# Setting up GitLab-CI und Docker Registry

Files for the [talk](https://programm.froscon.de/2017/events/1948.html) on setting up GitLab-CI with docker Registry on-premise

# Background

If you are using internal CA in your organisation and your GitLab instance is using a SSL certificate signed by this CA docker builds will fail pushing the results to GitLab due to non-trsuted SSL certificate. Workarbound is to add your organisation's root CA to the trusted list in the docker container run by GitLab-CI.

# Prerequisites

* Working GitLab instance
* Working GitLab Docker Registry

# Adjust GitLab-CI-runner configuration

**Without this DIND will not work!**

* edit /etc/gitlab-runner/config.toml
* add `"/var/run/docker.sock:/var/run/docker.sock:rw"` to the section `volumes`
* restart gitlab-multi-runner

```
[[runners]]
...
  executor = "docker"
  [runners.docker]
...
    privileged = true
    volumes = ["/cache", "/var/run/docker.sock:/var/run/docker.sock:rw"]
```

# Building docker image

To be able to build docker images using GitLab-CI you have to integrate your organisation's CA.

* create a group `gitlab-ci` in GitLab, which will contain your base images for CI
* create project `docker` and `dind` (Docker-in-Docker)
* enable registry for the projects
  * Settings->General->Container Registry
* assign GitLab-CI-runner to the projects
  * Settings->Pipelines->Available specific runners

Follow the documents:

* [docker:latest](docker-latest/README.md)
* [docker:dind](docker-dind/README.md)
* [example project](example-project/README.md)

# Scheduled builds (optional)

* You can schedule your pipelines (for example daily) to always have a current version from the upstream