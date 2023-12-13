# taiko_node
This guide will help you start up a Taiko RPC node

# Prerequisites
Docker is installed and running.
Git is installed.
If using Windows, you should install Git BASH or WSL to use as your terminal.
Meet the Geth minimum hardware requirements except for the storage requirement because Taiko nodes will require less storage. 
As of 2023-09-18 a node uses less than 10 GB. 100 GB should be future proof enough if you intend to run your node for a while.

# Steps
## 1. Clone simple-taiko-node
```
git clone https://github.com/taikoxyz/simple-taiko-node.git
```
```
cd simple-taiko-node
```
## 2. Copy the sample .env files
```
cp .env.sample .env
```
## 3. Set the required values in the .env file
### First, open the .env in your preferred text editor:
```
nano .env
```
## Next, you will set the L1 archive node endpoints.
#### You can use any Sepolia L1 endpoint, but it must point to an archive node to access the state trie beyond the last 128 blocks.
It's recommended to follow Local below, otherwise you may need to use a paid account for a Sepolia RPC provider. 
Alchemy and Infura will work temporarily, but will eventually rate limit the requests for a free account, and your node will stop syncing.
If you run into rate limit issues, many community members have had success by changing the HTTPS endpoint to https://rpc.sepolia.org.

## Local
If you are running a local Sepolia node, you cannot reference the L1 endpoints as http://127.0.0.1:8545 and ws://127.0.0.1:8546 because that is local to inside the simple-taiko-node Docker image. 
Depending on your firewall setup, you can do a few things. You can try:

- Using host.docker.internal (see: stack overflow)
- Using the private ip address of your machine (use something like ip addr show to get this ip address)

### Finally, set the following L1 node endpoints in your .env file:

- L1_ENDPOINT_HTTP
- L1_ENDPOINT_WS
  
Take a look at the comments above these values in the .env.sample to see how to set them up.

## 4. Start a node

### Make sure Docker is running and then run the following command to start the node:
```
docker compose up -d
```
### Note: You may need to use sudo docker compose up -d if you are not in the docker group.

If you ran a testnet node previously make sure to first run docker compose down -v to remove the old volumes.

