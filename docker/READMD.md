# Getting Started  with Docker

Docker image is available from https://hub.docker.com/r/neilsb/mx-puppet-teams
Docker-compose file is mainly used for local tests.
It has been build with a synapse image coming from https://hub.docker.com/r/matrixdotorg/synapse (see documentation)
And it first version is available here : https://github.com/matrix-org/synapse/blob/develop/contrib/docker/docker-compose.yml

- Edit your /etc/hosts file to map my.matrix.host to localhost  
    Add the following line to your /etc/hosts file
    ```shell
    127.0.0.1	my.matrix.host
    127.0.0.1	my.bridge.host
    ```
- set this folder as working directory
    ```shell
    cd docker/
    ```
- generate the homeserver.yaml configuration file for synapse 
    ```shell
    docker-compose run --rm -e SYNAPSE_SERVER_NAME=my.matrix.host -e SYNAPSE_REPORT_STATS=yes synapse generate
    ```
    this will result in following files created in the synapse_files folder :  

    - homeserver.db*
    - homeserver.yaml
    - my.matrix.host.log.config
    - my.matrix.host.singing.key

- copy paste the config file for the bridge and modify its values
    ```shell
    cp ../sample.config.yaml bridge_files/config.yaml
    ```
- generate the ms-registration.yaml file
    ```shell
    docker-compose run teams-bridge
    ```
  and stop the container with CTRL+C
- Then finally run the whole stack
    ```shell
    docker-compose up -d
    ```
