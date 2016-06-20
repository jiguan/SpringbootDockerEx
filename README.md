Name: Spring Boot with Docker
Description: This is a simple project about how to deploy a springboot application within a docker container.

Steps: 
1. Build image: mvn package docker:build
2. Run image: docker run -e "SPRING_PROFILES_ACTIVE=prod" -p 8080:8080 -t springio/spring-boot-docker
3. Access 192.168.99.100:8080 (Host address shows up when docker starts)

Notice: 
1. Dockerfile specifies the docker image. In the line "Add {artifactId}-{version}.jar app.jar", the artifactId and version should match the value in the pom.xml.
2. The image is under 'springio' directory. The name is specified under the pom.xml <docker.image.prefix> property.
3. The docker uses the generated image "springio/spring-boot-docker" but there is no such file under project directory. The location of docker images is under cocker's VM: ~/.docker/machine/machines/default
4. When starting the image, -p is port matching: local port : springboot port.
5. If you want to kill the application, use command: 'curl -X POST localhost:port/shutdown'. If you use control-c to terminate the application, the application is running inside docker. Use 'docker ps' and 'docker kill {NAME}' to kill the app.  
6. If showing up error message "docker Connect to localhost:2375 failed: Connection refused", it means 'DOCKER_HOST' variable is not set. Starting Docker quickstart terminal can fix this problem. 
