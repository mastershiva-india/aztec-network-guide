# aztec-network
A step by step guide on How to Run `Sequencer Node` on Aztec Network Testnet & Earn `Apprentice` Role.

## Hardware Requirements
* **Sequencer Node**: 8 cores CPU, 16GB RAM, 100GB+ SSD
* **Prover Node**: Requiring ~40x machines with 16 cores and 128GB RAM

You can get a 3months free vm intanse via gmail google.cloud.com
Use SSH client like termius : https://termius.com/ wich supports windows mac and Linux and android also.

Install Dependecies

Update Packages - command :

sudo apt-get update && sudo apt-get upgrade -y

Install Packages - command :

sudo apt install curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev  -y

Install Docker - command :
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Test Docker
sudo docker run hello-world

sudo systemctl enable docker
sudo systemctl restart docker
if you using google cloud than use 2nd command before 3rd command if you using normal vps than 3rd command directly!
usermod
sudo usermod -aG docker $USER
newgrp docker

NOW OPEN A NEW TERMINAL OR DUPLICATE
Install Aztec Tools
bash -i <(curl -s https://install.aztec.network)

Run this command again :
sudo usermod -aG docker $USER

Now update Aztec
aztec-up alpha-testnet

IF showing error like : aztec-up: command not found, then apply this command :
find $HOME -type f -name "aztec-up"
~/.aztec/bin/aztec-up alpha-testnet
Now Run Sequencer Node
Open new screen or duplicate
screen -S aztec 
9. Run

aztec-up alpha-testnet

Find IP
curl ipv4.icanhazip.com

### Run Node
aztec start --node --archiver --sequencer \
  --network alpha-testnet \
  --l1-rpc-urls RPC_URL  \
  --l1-consensus-host-urls BEACON_URL \
  --sequencer.validatorPrivateKey 0xYourPrivateKey \
  --sequencer.coinbase 0xYourAddress \
  --p2p.p2pIp IP
Replace the following variables before you Run Node:

RPC_URL & BEACON_URL: for RPC go to alchemy > and search/create a sepolia rpc url & go to ankr.com > to buy a beacon url
0xYourPrivateKey: Your EVM wallet private key
0xYourAddress: Your EVM wallet public address
IP: Your server IP (Step 10)

Create a new wallet ( metamusk/phantom etc wallet.
Add 0x before evm wallet private address

Optional Commands:

Screen Commands:
Minimze screen: Ctrl + A + D
Return to screen: screen -r aztec
Kill screen (when inside): Ctrl+C+ Kill screen (when outside): screen -XS aztec quit`

Sync Node
After entering the command, your node starts running, It takes a few minutes to 4hrs for your node to get synced.

Get Role
Go to the discord channel :[operators| start-here] and follow the prompts,
You can continue the guide with this commands if you need help join TG Group

Step 1: Get the latest proven block number:

curl -s -X POST -H 'Content-Type: application/json' \
-d '{"jsonrpc":"2.0","method":"node_getL2Tips","params":[],"id":67}' \
http://localhost:8080 | jq -r ".result.proven.number"
Here you get a number example output: 20905, Save this block number for the next steps

Step 2: Generate your sync proof

curl -s -X POST -H 'Content-Type: application/json' \
-d '{"jsonrpc":"2.0","method":"node_getArchiveSiblingPath","params":["BLOCK_NUMBER","BLOCK_NUMBER"],"id":67}' \
http://localhost:8080 | jq -r ".result"
Replace Both the BLOCK_NUMBER with your number

Step 3: Register with Discord

Type the following command in this Discord server: /operator start
After typing the command, Discord will display option fields that look like this:
address: Your validator address (Ethereum Address)
block-number: Block number for verification (Block number from Step 1)
proof: Your sync proof (base64 string from Step 2)
Then you'll get your Apprentice Role

*. If the proof is showing old then delete the previous data and re-run the node

Delete old data: rm -rf ~/.aztec/alpha-testnet/data/

Stop node with Ctrl+C.

Now Re-run the node : rm -r /root/.aztec/alpha-testnet

in TG group - https://t.me/Web3brothersFamily
My TG ID : @mastershivay
Any issue contact !
