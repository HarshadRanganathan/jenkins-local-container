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

You can use any of the `uid` and `userPassword` mentioned in `users.ldif` file for successful LDAP login.

e.g.
```text
username: user
password: changeit
```

`Note: Only superuser has access to view/edit Manage Jenkins page. Check authorizationStrategy matrix in jenkins.yaml file`

### Plugins

List of plugins to be installed is defined in `plugins.txt` file.

`Note: If you are running in windows, make sure that the plugins.txt file line ending is LF instead of CRLF. Otherwise, the plugin installation will fail with Illegal characters found in URL error`

### System Configuration

System configuration is defined in the file `jenkins.yaml`.

### LDAP

We run `SLDAP` service which is a stand-alone LDAP daemon. 

To administer the LDAP service, we make use of `phpLDAPadmin` which is a web-based LDAP client providing multi-language administration for your LDAP server.

`phpLDAPadmin` is available at http://localhost:8090/.


Login DN: cn=admin,dc=acme,dc=local

Password: changeit

![phpLDAPadmin](images/phpLDAPadmin.png?raw=true)