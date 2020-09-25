## Jenkins Local Container

Run Jenkins in your local as a docker container.

### Pre-Requisites

1. Docker
2. Make

### Execution

Run `make` which will execute the docker compose commands and start up the jenkins container at http://localhost:8080/

```shell
❯ make

docker-compose \
        --file docker-compose.yaml \
        down \
        --remove-orphans \
        --rmi local \
        --volumes
Removing network jenkins-local-container_default
Removing volume jenkins-local-container_jenkins_home
Removing image jenkins-local-container_jenkins
WARNING: Image jenkins-local-container_jenkins not found.
docker-compose \
        --file docker-compose.yaml \
        up \
        --build \
        --detach
Creating network "jenkins-local-container_default" with the default driver
Creating volume "jenkins-local-container_jenkins_home" with default driver
Building jenkins
```

### Plugins

List of plugins to be installed is defined in `plugins.txt` file.

`Note: If you are running in windows, make sure that the plugins.txt file line ending is LF instead of CRLF. Otherwise, the plugin installation will fail with Illegal characters found in URL error`