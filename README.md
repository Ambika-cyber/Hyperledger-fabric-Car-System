# Hyperledger Fabric Blockchain

Building a proof-of-concept on a customized permission network (Hyperledger Fabric). The network will have two peers and one orderer who help run and maintain the network (e.g., verify and endorse transactions), implemented one smart contract (Go programming language) with all the functionality needed to read and write the ledger. To interact with the network also implemented multiple applications (JavaScript).

## Fabric Blockchain Network:
The following command allows for starting a network with a communication channel (connecting each organization), a certificate authority (CA), and a database (Couchdb)

./network.sh up createChannel -ca -s couchdb


### Chaincode:

Chaincode (also called “smart contract”) initializes and manages the ledger state through transactions submitted by applications. Chaincode runs in a secured Docker container isolated from the endorsing peer process.

### Orderer:

The Orderer is responsible for packaging transactions into Blocks and distributing them to Anchor Peers across the network. This means the network will rely on deterministic consensus algorithms, any block validated by the peer is guaranteed to be final and correct.

### Channel:

A Channel is a private “subnet” of communication between two or more specific network members, for the purpose of conducting private and confidential transactions.

### Couchdb:

CouchDB is an optional, alternate state database that allows you to model data on the ledger as JSON and issue rich queries against data values rather than the keys. CouchDB runs as a separate database process alongside the peer.

### Certificate Authority:

The Certificate Authority (CA) provides a number of certificate services to users of a blockchain. More specifically, these services relate to user enrollment, transactions invoked on the blockchain and TLS-secured connections between users or components of the blockchain.

The CA and the Couchdb, both need to be defined when starting the network:

### JavaScript application:
The javascript application will allow to register users to the network and to interact with the smart contract to write data to the ledger.

Before using the applications, the enrollAdmin.js need to be executed to create the admin user. After that each user needs to be executed in their respective folder. This will create user wallets that allow to execute transaction in the network.

### Network demonstration:
Running the startFabric.sh script will start the network and create a ledger with a channel, a CA (Certificate Authority) and Couchdb. Then it will implement the smart contract and initialize the ledger:

### steps to run code:
Step 1: Copy the project folder into the fabric-samples folder of hyperledger fabric.

Step 2: Install all node modules in the javascrip folder 

	npm install 

Step 3: Create channel in fabric
            cd fabric-samples/test-network
             sudo ./network.sh down
             sudo ./network.sh up createChannel -c fabric-car -ca

Step 4: Deploy chaincode
    sudo ./network.sh deployCC -c carChannel -ccn carchaincode -ccp ../Fabric-Car/chaincode/ -ccl javascript

Step 4: Use application in the javascript folder to interact with the network
    node app.js

Step 5: Stop network by running networkDown.sh
