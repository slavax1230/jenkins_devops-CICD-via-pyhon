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
8. install docker plugin in jenkins available plugins
8. dashboard > managa jenkins > cloud > make new based docker
9. (in the project folder)

docker run -d --restart=always -p 127.0.0.1:2376:2375 --network jenkins -v /var/run/docker.sock:/var/run/docker.sock alpine/socat tcp-listen:2375,fork,reuseaddr unix-connect:/var/run/docker.sock

10. docker inspect <container_id> (the container id will be the strange name that docker give)
take the ipAdress from there and add it to host Docker host URI as: tcp://172.20.0.3:2375
11. make V on some field there (forgot the name)
12. in the cloud we maked do: 
configure > docker agent templates> add docker tamplate:
-labes:(just a name): Docker-agent-python
-name:Docker-agent-python
-docker image: ( here we can access to docker hub or get locally ): devopsjourney1/myjenkinsagents:python
- instace  capaciy: 2
- Remote File System Root:home/jenkins

13. select the project we made before in jenkins: jenkins-python
go to configure and select: Restrict where this project can be run
select the Cloud you made and build. now the services will run there.

14. go to BUILD Triggers in  configure:
select Build Periodicly: 
input: H/5 * * * * (will say run automaticly in some time.)







