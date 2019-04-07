# Hyperledger Fabric Multi-organization Setup

This repository demonstrates the Hyperledger Fabric Multi-Organization docker setup on single machine.

## Pre-requisites:
* [cURL](https://curl.haxx.se/download.html)
* [docker](https://www.digitalocean.com/community/tutorials/how-to-install-docker-compose-on-ubuntu-18-04)
* [Install Samples, Binaries and Docker Images](https://hyperledger-fabric.readthedocs.io/en/release-1.4/install.html)
* [Go](https://www.digitalocean.com/community/tutorials/how-to-install-go-on-ubuntu-18-04)

Check [this](https://hyperledger-fabric.readthedocs.io/en/release-1.4/getting_started.html) for more details.


## Network Setup Steps (without generating new certificates):

1. Clone the below repository
    ``` shell
    git clone https://github.com/rushikeshacharya/hyperledger-fabric.git
    ```

2. Chenge the branch to HLF-MultiOrgSetup
    ```shell
        git checkout HFL-MultiOrgSetup
    ```
3. go to the ORG1 directory and execute below command
    ```shell 
        cd ORG1
        ./start.sh
    ```
4.  Check whether the docker containers are running or not by executing below command
    ```shell
        docker ps
    ```
    * After executing above commad you will see the list of running docker containers.

5. Install and instantiate chaincode by executing below script:
    ```shell
        ./installChaincode.sh
    ```
    * This script will install chaincode in ORG1 and instantiate on mychannel

6. Invoke the chaincode by executing below script:
    ```shell
        ./createCar.sh
    ```
7. Query chaincode by executing below script:
    ```shell
        ./query.sh
    ```

You can change the values in createCar.sh and query.sh for different result.

For ORG2

8. cd into ORG2 and execute below script:
    ```shell
        ./start.sh
    ```
9. check the docker containers by running `` docker ps ``

10. Now install chaincode on ORG2 by running below script
    ```shell
        ./installChaincode.sh
    ```
11. Now invoke chaincode functions by executing below script:
    ```shell 
        ./createCar.sh
    ```
    * Only first time this script will take time, because whenever chaincode gets invoked first time, docker container will get created for chaincode.

12. Check the result by executing below command:
    ```shell
        ./query.sh
    ```     
___

## Network Setup Steps (Generating new certificates)

1. cd into scripts directory and execute belwo scripts:
    ```shell
        ./generate.sh
    ```
    
2. 