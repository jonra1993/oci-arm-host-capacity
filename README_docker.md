# oracle-tf
### [source and config](https://github.com/hitrov/oci-arm-host-capacity)

* build Dockerfile
  * $ docker build  -t jrtec/oci-arm-host:latest .
  * $ docker push jrtec/oci-arm-host:latest
  * $ docker buildx build --platform linux/arm64,linux/amd64 -t jrtec/oci-arm-host:latest -o type=registry .


### Build local whith DockerfilePerformance, edit DockerfilePerformance to first image
  * $ docker login
  * Fisrt and Second___: docker buildx build --platform linux/arm64,linux/amd64 -f DockerfilePerformance -t DOCKER/IMAGENAME:IMAGETAG -o type=image .  
  * Thirt______________: docker buildx build --platform linux/arm64,linux/amd64 -f DockerfilePerformance -t DOCKER/IMAGENAME:IMAGETAG -o type=registry . 

### run
  * default RETRY_DELAY_TIME 10 minutes
    * $ docker run --rm -d \
        -v $(pwd)/.env:/app/oci-arm-host-capacity/.env \
        -v $(pwd)/key.pem:/app/oci-arm-host-capacity/key.pem \
        jrtec/oci-arm-host

  or
  
  * to set RETRY_DELAY_TIME = 5 minutes
    * $ docker run --rm -d \
        -e RETRY_DELAY_TIME=5 \
        -v $(pwd)/.env:/app/oci-arm-host-capacity/.env \
        -v $(pwd)/key.pem:/app/oci-arm-host-capacity/key.pem \
        jrtec/oci-arm-host

  * to set RETRY_DELAY_TIME = 5 minutes
    * $ docker run --rm -d -e RETRY_DELAY_TIME=5 -v $(pwd)/.env:/app/oci-arm-host-capacity/.env -v $(pwd)/oci/oracleidentitycloudservices.pem:/app/oci-arm-host-capacity/key.pem jrtec/oci-arm-host

  * to set RETRY_DELAY_TIME = 5 minutes
    * $ docker run --rm -d -e RETRY_DELAY_TIME=5 -v $(pwd)/.env:/app/oci-arm-host-capacity/.env -v $(pwd)/oci/oracleidentitycloudservices.pem:/app/oci-arm-host-capacity/key.pem jrtec/oci-arm-host 

    docker run --rm -e RETRY_DELAY_TIME=5 -v $(pwd)/.env:/app/oci-arm-host-capacity/.env -v $(pwd)/oci/oracleidentitycloudservices.pem:/app/oci-arm-host-capacity/key.pem jrtec/oci-arm-host 

### Github action - .github/workflows/docker-image.yml
  * add secret - github.com > project > settings > Secrets > Actions
    * DOCKER_NAMESPACE
    * DOCKER_PASSWORD
      * create a token on user settings
    * DOCKER_REPOSITORY
    * DOCKER_USERNAME  