# Jenkins Docker Compose build instructions

Create an ssh key using:
```ssh-keygen -t rsa -f jenkins_agent```

Set the environment variable of the jenkins agent to the public key.
Add the private key to jenkins credentials after the initial setup. 


Additional settings for the node:

Remote root directory: */home/jenkins/agent*

Launch method: *Launch agents via SSH*

Host: *agent*

Credentials: The one you added before

Host Key Verification Strategy: *Non verifying*

JavaPath: */opt/java/openjdk/bin/java*


[Credit to this guide](https://www.cloudbees.com/blog/how-to-install-and-run-jenkins-with-docker-compose)


## Old Commands, kept for reference

docker build -t jenkins .

docker run --name jenkins-docker --rm --detach --privileged --network jenkins --network-alias docker --env DOCKER_TLS_CERTDIR=/certs --volume jenkins-docker-certs:/certs/client --volume jenkins-data:/var/jenkins_home --publish 2376:2376 docker:dind

docker run --name jenkins --restart=on-failure --detach --network jenkins --env DOCKER_HOST=tcp://docker:2376 --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 --volume jenkins-data:/var/jenkins_home --volume jenkins-docker-certs:/certs/client:ro --publish 3003:8080 --publish 50000:50000 jenkins
