# Create an image localy and push it to the registry

* login to your docker registry
  * `docker login docker-registry.yourdomain.com`
* clone this repo
* `cd docker-latest`
* put your CA in `my_ca.crt` in PEM format
* `docker build -t docker-registry.yourdomain.com/gitlab-ci/docker:master .`
* `docker push docker-registry.yourdomain.com/gitlab-ci/docker:master`
* copy the files in this directory to your repository named `docker` and push the cahnges to GitLab

