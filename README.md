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

`Note: Only superuser has access to create jobs and manage jenkins settings. Check authorizationStrategy matrix in jenkins.yaml file for more details`

### Plugins

List of plugins to be installed is defined in `plugins.txt` file.

`Note: If you are running in windows, make sure that the plugins.txt file line ending is LF instead of CRLF. Otherwise, the plugin installation will fail with Illegal characters found in URL error`

### System Configuration

System configuration is defined in the file `jenkins.yaml`.

### LDAP

We run `SLDAP` service which is a stand-alone LDAP daemon. 

To administer the LDAP service, we make use of `phpLDAPadmin` which is a web-based LDAP client providing multi-language administration for your LDAP server.

`phpLDAPadmin` is available at http://localhost:8090/.

```text
Login DN: cn=admin,dc=acme,dc=local
Password: changeit
```

You can view the users and groups configured for Jenkins LDAP access here.

![phpLDAPadmin](images/phpLDAPadmin.png?raw=true)

### Nexus

Nexus is available at http://localhost:8081/

Get the admin password by running below command:

```shell
docker exec -it \
 $(docker ps --filter "name=nexus_1" --quiet)  \
 bash -c "cat /nexus-data/admin.password && echo"
```

Login to the console using the above password and username as `admin`.

In the wizard, change the password and check `Enable anonymous access` so that we can access the artifacts without credentials.