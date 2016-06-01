###Spring Boot with Docker
This is a simple project to try how to deploy a springboot application within a docker container.

####Steps: 
  1. Build image: `mvn package docker:build`
  2.  Run image: `docker run -e "SPRING_PROFILES_ACTIVE=prod" -p 8080:8080 -t springio/spring-boot-docker`
  3. Access `192.168.99.100:8080` (Host address shows up when docker starts)

####Notice: 
* `Dockerfile` specifies the docker image. In the line `Add {artifactId}-{version}.jar app.jar`, the artifactId and version should match the value in the pom.xml.
* The image is under `springio` directory. The name is specified under the pom.xml `<docker.image.prefix>` property.
* The docker uses the generated image `springio/spring-boot-docker` under docker's VM: `~/.docker/machine/machines/default`
* When running the image, `-p` specifies port matching: `{LOCAL_PORT}` : `{APP_PORT}`.
* If you want to kill the application, use the command: `curl -X POST localhost:port/shutdown`. If using control-c to terminate the application, the application is still running inside the docker. In this case, use `docker ps` and `docker kill {NAME}` to kill the app.  
* If showing up error message "docker Connect to localhost:2375 failed: Connection refused", it means `DOCKER_HOST` variable is not set. Starting Docker quickstart terminal can fix this problem. 
