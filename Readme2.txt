1. git clone 
2. docker build -t jenkins-cicd:1.0.0 .
3. docker network create jenkins
4.

docker run --name jenkins-blueocean --restart=on-failure --detach `
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 `
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 `
  --volume jenkins-data:/var/jenkins_home `
  --volume jenkins-docker-certs:/certs/client:ro `
  --publish 8084:8080 --publish 50000:50000 jenkins-blueocean

5.

docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword

6. open new project in jenkins:
7. change the branch name from master to main in jenkins