# Philosophy
## Decentralisation
* No central authority
* No central server
* Everything must run on single-board PC like raspbery PI
## Microservices
* Thin service - thick client
* Many services for different needs
* The server with microservices is called Node
## Registration in blockchain
* Every user has one or many keypairs and one current keypair
* User info and user public keys are stored in blockchain
* Node info and node public key are stored in blockchain
## Encryption
* User has keypair(s) to encrypt-descrypt messages and files also sign messages and files.
* The communication between User and User is encrypted and signed also communication between User and Node is encrypted and signed
* The user also can have simmetrical ciphers for different purpuses.
* The Node does not see communication between Users
## Coin-Hours as a payment system
The Ness Coins generate Coin-Hours and it is main payment method. 
The User pays with Coin-Hours for time he user the Node.
# Installation
The Node works on the top of Emercoin and Privateness blockchains.

To install your Node and test it with your User you must do the following:
* Generate User and it's keys
* Generate Node and it's keys
* Generate Node config files
* Install Emercoin wallet
* Add User and Node records in Emercoin Blockchain
* Install Privateness client
* Install Web Server
* Clone Node from GIT repository into configured Web Server directory
* Copy Node config files into ~/.ness directory and edit config files to enstablish connection to Privateness and Emercoin daemons
* RUN Emercoin daemon, Privateness daemon, WEB Server and test the node manualy with WEB browser and with Node Tester.
## Node and user generation
### Install Node tester
You need to install Ness Node Tester to generate NODE or and USER.
Both USER and NODE needs to be registered in blockchain and NODE.
`git clone https://github.com/NESS-Network/NessNodeTester`
install dependencies:
`pip install requests pynacl pycryptodome validators lxml`
### Node generation
#### Script
###### Node generation
`python codegen.py -ng http://my-ness-node.net 24 master-user-name "Test,My test node,Hello world"`
OR
`python codegen.py --node-generate http://my-ness-node.net 24 master-user-name "Test,My test node,Hello world"`
Where
* `http://my-ness-node.net` - node URL
* `"Test,My test node,Hello world"` - coma separated tags
* `24` - tariff, ammount of NCH payed to node (master-user address) every 24 hours
* `master-user-name` - username of existing user, which will became owner of funds of this node
The generated node keys will be placed in `out/node/keys` directory
##### Show generated node data
`python codegen.py -ns http://my-ness-node.net`
OR
`python codegen.py --node-show http://my-ness-node.net`
##### Show generated content for blockchain
`python codegen.py -nsw http://my-ness-node.net`
OR
`python codegen.py --node-show-worm http://my-ness-node.net`
This command will show generated WORM markup to be placed in blockchain.
##### Configuration generation for node
`python configen.py http://my-ness-node.net`
The generated config will be placed in `out/config` directory
#### Blockchain record
*Emercoin blockchain NVS record:*
NAME: 
`worm:node:ness:http://my-ness-node.net`
VALUE:
```xml
<worm>
        <node type="ness" url="http://my-ness-node.net" nonce="Q3khjWopdxiLpPweVo6+BQ=="    verify="Q13IcdGM6CLjH+zZ/EaPgK+2C8igkh8/x0aEgZVVfTw=" public="dJplXPV7cqsC518qg0bJXoWknhqkIZQNTnksVHaSq2E=" master-user="master-user-name" tariff="24" tags="Test,My test node,Hello world">
                <!-- Here tags may be different for each type of node or each node -->
        </node>
</worm>
```
* *type* must be "ness"
* *url* - URL address of node
* *nonce* - random cryptographic salt
* *public* - public key
* *verify* - verify key
* *master-user* - name of node admin (admin can withdraw funds earned by funds)
* *tariff* - tariff, ammount of NCH payed to node (master-user address) every 24 hours
### User generation
#### Script
###### User generation
`python codegen.py -ug username 10 "1,blowfish,16;1,aes,8" "Hello World,test"`
OR
`python codegen.py --user-generate username 10 "1,blowfish,16;1,aes,8" "Hello World,test"`
##### Show generated user data
`python codegen.py -us username`
OR
`python codegen.py --user-show username`
##### Show generated content for blockchain
`python codegen.py -usw username`
OR
`python codegen.py --user-show-worm username`
#### Blockchain record
*Emercoin blockchain record:*
NAME:
`worm:user:ness:user`
VALUE:
```xml
<worm>
        <user type="ness" nonce="R04rQis5hP2EfILpAGuU8Q==" tags="Hello World,test">
                <keys>
                        <key public="rGSy2GhojuHX+4bgE5CtRZnP2OpR7+RJebqGDCNVnlY="  verify="n9SUQ3w4x+YBggUqlN/e26lopaE2rCLmOZK9Cg2zRtc=" current="current" />
                        <key public="61RxrG8CIOSDfcjLcq+y/dhhMgeyY9I7NdDZTaoQwUs="  verify="FhnIDQZ1XDOaspV4/k+ZADSe5IqkUQCWH53C42qC3XQ="/>
                        <key public="0DThVjUslwgoZuclc0ueKZYl7r+4rfmUw2bWShyQYU0="  verify="wsvQ8HXjG3P4v9+xhnp1Nc8XhLCTb0WbK3cq9aOCHZk="/>
                        <key public="QVXITMyfQLg5tVc+ElpVX0FAN3+/nv9nGZDUIVUbiwo="  verify="UZz4azAIqO2WiNMkgkgCMu38Sw8WEOco8C6y3R2Lyuk="/>
                        <key public="8QHSSL2Hgsm6wfSFaFD+6ODW770Pr8+rdABwGKBo8WA="  verify="xQHkzmniUIDTCFWWOpA9tYzmlF+AmBHCPH5mMSZF+Bw="/>
                        <key public="EaD4ufAdkRlW7psqAhL+DrGmIVQvR+R9DiaTKzoO4Eg="  verify="wkkDp9PZWj6Dq+65Xjs42zCwkz5BWJvzQt4TE9kIc7o="/>
                        <key public="kTsf7ZKy0urSGklAxLJWbHOjFtCgFlXSEq4dHDl4GEw="  verify="A2bw4W8CNr2NXBsyDLIrobJh997u90ziaSX1HJTyJNA="/>
                        <key public="HZGLPz9PukobSM6ALz7PxqBYunimLkqAoa2WwAGrDB8="  verify="gNz9z6ZOcXJgDm1BWbRrCkz4HWJ3EB4IKAO4u/imjTU="/>
                        <key public="rYsglIKg2ZQf4yfmqjH70vaC0wCjO5mXAdHPwaWcOX4="  verify="1iC81pdum1JRgQ/9j9ceu5QsPVo5VpUjAmwY6LQPM+4="/>
                </keys>
                <!-- Here tags may be different for each type of user -->
        </user>
</worm>
```
* verify - verify public key
* public - encryption public key
* nonce - random cryptographic salt
### PRNG service instalation (optional)
`git clone https://github.com/NESS-Network/PyUHEPRNG`
`cd PyUHEPRNG/`
Now run the server and it will generate files with random data
`python server.py`

## Node environment
***
#### Install Privateness wallet
`git clone https://github.com/NESS-Network/privateness`
Execute
`./run-client.sh`
to run Privateness daemon

### For Debian
***
### For Arch
***
### Copy keys and config files
Execute console commands:
`mkdir ~/.ness`
`cp out/config/*.json ~/.ness`
#### Config files
* *emer.json* - connection to emercoin RPC
* *ness.json* - Connection to Privateness wallet-daemon
* node.json - auto-generated Node config (URL, tariff and public keys)
* prng.json - PRNG service config (file locations)
* users_addr.json - Node users and their addresses (auto-generated)
## Web server
You must have Apache or other web server (Tested on Apache)
### Check that node is running
Goto `http://node-url/node/info` and if everything is correct, you will see information about current node in JSON format
### Services
All output is made in JSON format. if param `result` is `error` then the error message is stored in `error` param as string if param `result` is `info` then the info is stored in `info` param as array if param `result` is `data` then the data is stored in `data` param as array

All data is sent in HTTP POST or GET request and returned in JSON format

Read more about authentication [here](https://ness-main-dev.medium.com/authentication-on-ness-nodes-f25e2cda0f0d) and [here](https://ness-main-dev.medium.com/file-service-412bbe6f26a8)
#### Node service
Node service is for node administration and displaying service data.

Read more about Node service [here](https://github.com/NESS-Network/NessNode#node)

#### PRNG service
PRNG service is for getting random data from node.

Read more about PRNG service [here](https://github.com/NESS-Network/NessNode#prng)

#### Files service

This service can upload, download and store files

Read more about Files service [here](https://ness-main-dev.medium.com/file-service-412bbe6f26a8) and [here](https://ness-main-dev.medium.com/shadowname-4cba73b41a5d)

#### IPFS service
Not implemented yet ...
