# ProfitBricks Docker Machine Driver

The ProfitBricks Docker Machine Driver is a plugin for Docker Machine which allows you to automate the provisioning of Docker machines on ProfitBricks servers. This is the official Docker Machine driver for ProfitBricks.

### Requirements

*  [Docker Machine](https://docs.docker.com/machine/install-machine/)

## Installation

Run the following commands to install the ProfitBricks Docker Machine driver:

    go get github.com/profitbricks/docker-machine-driver-profitbricks
    cd $GOPATH/src/github.com/profitbricks/docker-machine-driver-profitbricks
    make install  

## Usage

You may want to refer to the Docker Machine [official documentation](https://docs.docker.com/machine/) before using the driver.

### Create a ProfitBricks Machine

Before you create a ProfitBricks machine you will need to set these variables:

    export PROFITBRICKS_USERNAME="profitbricks_username"
    export PROFITBRICKS_PASSWORD="profitbricks_password"

Then run this command to create a machine:

    docker-machine create --driver profitbricks test-machine

To get detailed information about the possible options,  run the command:

    docker-machine create --help --driver profitbricks

Available options:

* `--driver`, `-d` "none": Driver to create machine with.
* `--engine-env [--engine-env option --engine-env option]`: Specify environment variables to set in the engine.
* `--engine-insecure-registry [--engine-insecure-registry option --engine-insecure-registry option]`: Specify insecure registries to allow with the created engine.
* `--engine-install-url "https://get.docker.com"` Custom URL to use for engine installation [$MACHINE_DOCKER_INSTALL_URL].
* `--engine-label [--engine-label option --engine-label option]`: Specify labels for the created engine.
* `--engine-opt [--engine-opt option --engine-opt option]`: Specify arbitrary flags to include with the created engine in the form flag=value.
* `--engine-registry-mirror [--engine-registry-mirror option --engine-registry-mirror option]`: Specify registry mirrors to use.
* `--engine-storage-driver`: Specify a storage driver to use with the engine
* `--profitbricks-cores "4"`: ProfitBricks cores (2, 3, 4, 5, 6, etc.) [$PROFITBRICKS_CORES].
* `--profitbricks-disk-size "50"`: ProfitBricks disk size (10, 50, 100, 200, 400) [$PROFITBRICKS_DISK_SIZE]
* `--profitbricks-disk-type "HDD"`: ProfitBricks disk type (HDD, SSD) [$PROFITBRICKS_DISK_TYPE].
* `--profitbricks-endpoint "https://api.profitbricks.com/rest/v2"`: ProfitBricks API endpoint [$PROFITBRICKS_ENDPOINT].
* `--profitbricks-image "Ubuntu-15.10-server-2016-03-01"`: ProfitBricks image [$PROFITBRICKS_IMAGE].
* `--profitbricks-location "us/las"`: ProfitBricks location [$PROFITBRICKS_LOCATION].
* `--profitbricks-password`: ProfitBricks password [$PROFITBRICKS_PASSWORD].
* `--profitbricks-ram "2048"`: ProfitBricks ram (1024, 2048, 3072, 4096, etc.) [$PROFITBRICKS_RAM].
* `--profitbricks-username`: ProfitBricks username [$PROFITBRICKS_USERNAME].
* `--swarm`: Configure Machine with Swarm.
*  `--swarm-addr`: addr to advertise for Swarm (default: detect and use the machine IP).
*  `--swarm-discovery`: Discovery service to use with Swarm.
* `--swarm-host "tcp://0.0.0.0:3376"`: IP/socket to listen on for Swarm master.
* `--swarm-image "swarm:latest"`: Specify Docker image to use for Swarm [$MACHINE_SWARM_IMAGE].
* `--swarm-master`: Configure Machine to be a Swarm master.
* `--swarm-opt [--swarm-opt option --swarm-opt option]`: Define arbitrary flags for Swarm.
* `--swarm-strategy "spread"`: Define a default scheduling strategy for Swarm.
* `--tls-san [--tls-san option --tls-san option]`: Support extra SANs for TLS certs.   


To list the machines you have created, use the command:

    docker-machine ls

It will return information about your machines, similar to this:

```
NAME           ACTIVE   DRIVER         STATE     URL                         SWARM   DOCKER    ERRORS
default        -        virtualbox     Running   tcp://192.168.99.100:2376           v1.10.2   
test-machine   -        profitbricks   Running   tcp://162.254.26.156:2376           v1.10.3   

```

# Create a Swarm of ProfitBricks Machines 

Before you create a swarm of ProfitBricks machines, run this command:

    docker run --rm swarm create

Use the output from this command to create the swarm and set a swarm master:

    docker-machine create -d profitbricks --swarm --swarm-master —-swarm-discovery token://f3a75db19a03589ac28550834457bfc3 swarm-master-test

To create a swarm child, use the command:

```docker-machine create -d profitbricks --swarm —-swarm-discovery token://f3a75db19a03589ac28550834457bfc3 swarm-child-test```


## Support

You are welcome to contact us with questions or comments at [ProfitBricks DevOps Central](https://devops.profitbricks.com/). Please report any issues via [GitHub's issue tracker](https://github.com/profitbricks/docker-machine-driver-profitbricks/issues).
