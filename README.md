# Hyperledger Fabric Multi-organization Setup

This repository demonstrates the Hyperledger Fabric Multi-Organization docker setup on single machine.

## Pre-requisites:
* [cURL](https://curl.haxx.se/download.html)
* [docker](https://www.digitalocean.com/community/tutorials/how-to-install-docker-compose-on-ubuntu-18-04)
* [Install Samples, Binaries and Docker Images](https://hyperledger-fabric.readthedocs.io/en/release-1.4/install.html)
* [Go](https://www.digitalocean.com/community/tutorials/how-to-install-go-on-ubuntu-18-04)

Check [this](https://hyperledger-fabric.readthedocs.io/en/release-1.4/getting_started.html) for more details.
___
## Understanding different **.yaml** files
1. [docker-compose.yaml](https://github.com/rushikeshacharya/hyperledger-fabric/blob/HFL-MultiOrgSetup/docs/docker-compose.README.md)
2. [crypto-config.yaml](https://github.com/rushikeshacharya/hyperledger-fabric/blob/HFL-MultiOrgSetup/docs/crypto-config.README.md)
3. [configtx.yaml](https://github.com/rushikeshacharya/hyperledger-fabric/blob/HFL-MultiOrgSetup/docs/configtx.README.md)

___

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
    * This script will install chaincode on peer0 of ORG1 and instantiate it on the mychannel

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
    cd scripts
    ./generate.sh
    ```
   * This scrip will generate certificates required to setup the network.
   * 

2. Go to the below directory : 
    ```shell
    cd ORG1/crypto-config/peerOrganizations/org1.example.com/ca
    ```
    * and copy the **filename** ending with **_sk** i.e 
    ```
    387f77ed2453442f65ecf659d77c0d28af2030819020d5b40d860b0f96a0bf7f_sk
    ```

3. Now open the docker-compose.yaml file and replace it with the existing value `fabric-ca-server-config`, which is present in 
    ```yaml
    services:
      ca.example.com:
    image: hyperledger/fabric-ca
    environment:
      fabric-ca-server-config/8f4608d294f2691cabb7171f7c64d759e388a66500b2dc06598d26f21720573a_sk
    ```
4. Now from **ORG1** directory run the below script:
    ```
    ./start.sh
    ```
    * Check whether the docker containers are running or not by executing below command
    ```shell
    docker ps
    ```
5. Install and instantiate chaincode by executing below script:
    ```shell
    ./installChaincode.sh
    ```
    * This script will install chaincode on peer0 of ORG1 and instantiate it on the mychannel.

6. Invoke the chaincode by executing below script:
    ```shell
    ./createCar.sh
    ```
7. Query chaincode by executing below script:
    ```shell
    ./query.sh
    ```

You can change the values in createCar.sh and query.sh for different result.

**For ORG2**

8. From ORG2 directory execute below script:
    ```shell
    ./start.sh
    ```
9. check the docker containers by executing `` docker ps ``

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