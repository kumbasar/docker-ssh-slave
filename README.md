# Jenkins SSH slave Docker image

[`jenkins/ssh-slave`](https://hub.docker.com/r/jenkins/ssh-slave/)

A [Jenkins](https://jenkins-ci.org) slave using SSH to establish connection to support dotnet sdk, Cloud Foundry CLI and git.

See [Jenkins Distributed builds](https://wiki.jenkins-ci.org/display/JENKINS/Distributed+builds) for more info.

## Running

To run a Docker container

```bash
export PUBLICKEY=`cat ~/.ssh/id_rsa.pub`
docker build -t ssh-slave:latest .
docker run -p 22222:22 -t ssh-slave:latest "${PUBLICKEY}"
```

To test the ssh connection

```bash
ssh jenkins@localhost -p 22222
```

You'll then be able to connect this slave using ssh-slaves-plugin as "jenkins" with the matching private key.

### How to use this image with Docker Plugin

To use this image with [Docker Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Docker+Plugin), you need to
pass the public SSH key using environment variable `JENKINS_SLAVE_SSH_PUBKEY` and not as a startup argument.

In _Environment_ field of the Docker Template (advanced section), just add:

    JENKINS_SLAVE_SSH_PUBKEY=<YOUR PUBLIC SSH KEY HERE>

Don't put quotes around the public key. You should be all set.
