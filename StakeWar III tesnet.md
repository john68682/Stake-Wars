# StakeWars Event Guide:Episode III

Event Info: Stake Wars is a program to familiarize the community with what it means to be a NEAR validator, and gives the community early access to a Chunk-only producer

Time: July 13 — September 9, 2022

Audience: Anyone can join at any time during the event period, but please join as soon as possible to take advantage of the program’s benefits

I.Challenge 001.md:
Configuration requirements:

![1](https://user-images.githubusercontent.com/108926478/180350787-02755f3e-3ad1-4034-bfe1-fc6146c8550b.png)

i bought 1 private VPS on Contabo for a reasonable price.

![2](https://user-images.githubusercontent.com/108926478/180350788-74dc4ea8-993b-4e77-bcec-527f3f7f4ec8.jpg)

Create a Wallet:

Create your own Shardnet wallet: https://wallet.shardnet.near.org/

![3](https://user-images.githubusercontent.com/108926478/180350789-e4d7d0ea-8233-45fd-ae10-5dfa2ad9a842.png)

!Note: The NEAR tokens given away are not real.

Updating Linux machines:

sudo apt update && sudo apt upgrade -y

![4](https://user-images.githubusercontent.com/108926478/180350792-06aceadb-fea3-4797-ab61-dcd0fec86feb.png)

Install developer tools, Node.js, and npm:

curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash —

apt install build-essential nodejs

PATH=”$PATH”

![5](https://user-images.githubusercontent.com/108926478/180350793-aac2df1f-e914-4835-ae48-d8ca6182b82b.png)

Test:


Install NEAR-CLI:

sudo npm install -g near-cli

![6](https://user-images.githubusercontent.com/108926478/180350794-71edbefc-939b-4520-ad29-08f38f0b9af9.png)

Now NEAR-CLI is installed!

We will set up Shardnet environment for Chunk-only producer:Create Shardnet Environment

export NEAR_ENV=shardnet

![7](https://user-images.githubusercontent.com/108926478/180350796-0a003070-01dd-415e-8277-179b638b8d30.png)

Then:

echo ‘export NEAR_ENV=shardnet’ >> ~/.bashrc

![8](https://user-images.githubusercontent.com/108926478/180350798-178afbbc-571b-48e2-834b-1babf8b6888b.png)

You can check other NEAR CLI Command Guides here: https://github.com/near/stakewars-iii/blob/main/challenges/001.md

II.Challenge 002.md

Make sure your VPS’s CPU is supported

lscpu | grep -P ‘(?=.*avx )(?=.*sse4.2 )(?=.*cx16 )(?=.*popcnt )’ > /dev/null \
&& echo “Supported” \
|| echo “Not supported”

![9](https://user-images.githubusercontent.com/108926478/180350801-5176fcfe-07c6-42be-ad81-d8f013922227.png)

Install developer tools:

sudo apt install -y git binutils-dev libcurl4-openssl-dev zlib1g-dev libdw-dev libiberty-dev cmake gcc g++ python docker.io protobuf-compiler libssl-dev pkg-config clang llvm cargo

![10](https://user-images.githubusercontent.com/108926478/180350802-29cbdeb6-73bd-47e9-8847-c9814897bd8a.png)

Install Python pip:

sudo apt install python3-pip

![11](https://user-images.githubusercontent.com/108926478/180350804-576895e2-7a8b-455f-a41e-92e406b9f7b7.png)

### Configure:

USER_BASE_BIN=$(python3 -m site — user-base)/bin

export PATH=”$USER_BASE_BIN:$PATH”

Install Building Env:

sudo apt install clang build-essential make

Install Rust & Cargo:

curl — proto ‘=https’ — tlsv1.2 -sSf https://sh.rustup.rs | sh

![12](https://user-images.githubusercontent.com/108926478/180350805-894404f0-dfcc-434c-8c9e-1b249ee5901d.png)

Hit “y” and enter

![13](https://user-images.githubusercontent.com/108926478/180350809-9dd94248-a5a9-4d6f-a355-0c4d956c1d59.png)

Press 1 and ENTER

Then:

source $HOME/.cargo/env

Clone nearcore from Github:

git clone https://github.com/near/nearcore
cd nearcore
git fetch

![14](https://user-images.githubusercontent.com/108926478/180350810-a6c3f9e6-0576-49cf-b745-824e9cf365c6.png)

Checkout to the commit needed. Please refer to the latest commit in Event Discord

git checkout <commit>

For now it will be

git checkout 8448ad1eb

![15](https://user-images.githubusercontent.com/108926478/180350815-3aaed0ba-f58f-457a-b7c8-13fb71fdca99.png)

Then execute this command:

cargo build -p neard — release — features shardnet

![16](https://user-images.githubusercontent.com/108926478/180350819-62a752cc-ed54-49dc-9a86-13da8f9ed04d.png)

It will take 7–10 mins to complete.

Then:Initialize working directory

./target/release/neard — home ~/.near init — chain-id shardnet — download-genesis

![17](https://user-images.githubusercontent.com/108926478/180350820-79e1b522-a53e-48ef-8673-07cdaf0293ea.png)

It will create a directory structure and will create config.json, node_key.json and genesis.json on the network you passed.

Replace config.json

rm ~/.near/config.json
wget -O ~/.near/config.json https://s3-us-west-1.amazonaws.com/build.nearprotocol.com/nearcore-deploy/shardnet/config.json

![18](https://user-images.githubusercontent.com/108926478/180350824-6f0dfc4f-f769-4f80-9bdd-d1fc13f5ed79.png)

Get the latest snapshot (this part will be skipped because after Hardfork on shardnet during 2022–07–18, it’s not required)

Install AWS CLI

sudo apt-get install awscli -y

![19](https://user-images.githubusercontent.com/108926478/180350826-235d62e0-a918-49aa-bea3-3f9427b0d8fc.png)

Next We activating the node as validator

A full access key needs to be installed locally to be able to sign transactions via NEAR-CLI.

Wallet Login:

Execute command:

Near Login
Copy the link to the browser: (Drag and highlight and right click to copy — don’t press Ctrl+c):

![20](https://user-images.githubusercontent.com/108926478/180350830-957de51c-15c5-418b-a41e-f889da3d0389.png)

2.Then hit “next” and “connect”

Then enter your accountID and hit “confirm”

![21](https://user-images.githubusercontent.com/108926478/180350831-eedf37aa-cbe2-4d98-b04f-05403a6fec5c.png)

3. Then the browser will appear as follows:

![22](https://user-images.githubusercontent.com/108926478/180350832-741d1096-ebb8-49a0-aee0-4a52f76a1db6.png)

4. Go back and enter your Shardnet wallet address and you will get the message:

![23](https://user-images.githubusercontent.com/108926478/180350834-6b6fdecc-4d56-449e-a9d2-dcd8aff832d8.png)

when successfully, we are good to go

Check the validator_key.json

cat ~/.near/validator_key.json

Replace the <pool_id> with your pool ID, for example

near generate-key hoang51993.factory.shardnet.near

Generate validator_key file from your wallet:

cp ~/.near-credentials/shardnet/YOUR_WALLET.json ~/.near/validator_key.json

Edit validator_key: Change “private_key” to “secret_key”:

nano $HOME/.near/validator_key.json

{
“account_id”:”xx.factory.shardnet.near”,”
public_key”:”ed25519:47KQrU**************************************”,
“secret_key”:”ed25519:***************************************************************************************”
}

Use this command:

sudo nano ~/.near/validator_key.json

![24](https://user-images.githubusercontent.com/108926478/180350766-7332ddd9-0288-4a55-9afe-b8e345926fdb.PNG)

Then hit Ctrl + O to write out and hit Ctrl +X to exit

Now setup System Command

sudo nano /etc/systemd/system/neard.service

and paste this

[Unit]
Description=NEARd Daemon Service

[Service]
Type=simple
User=<USER>
#Group=near
WorkingDirectory=/home/<USER>/.near
ExecStart=/home/<USER>/nearcore/target/release/neard run
Restart=on-failure
RestartSec=30
KillSignal=SIGINT
TimeoutStopSec=45
KillMode=mixed

[Install]
WantedBy=multi-user.target

Note: Change USER to your paths

![25](https://user-images.githubusercontent.com/108926478/180350770-4be1578c-9280-4bfd-9c40-675a246186f1.png)

Then Ctrl +O to save and Ctrl +X to exit

Check Logs:

journalctl -n 100 -f -u neard

![26](https://user-images.githubusercontent.com/108926478/180350773-e697f4e6-59c2-457a-8b1b-84a79af8ae61.png)

To get out hit Ctrl + C

Make log output in pretty print:

Setup: CCZE

sudo apt install ccze

![27](https://user-images.githubusercontent.com/108926478/180350779-6fc29176-3fe3-4a3b-9326-250c259160cd.png)

View Logs with color:

journalctl -n 100 -f -u neard | ccze -A

![28](https://user-images.githubusercontent.com/108926478/180350781-ed82b075-322d-4181-9451-7905028a73e1.png)

To get out hit Ctrl + C

III.Challenge 003.md:

Deploy Staking pool:

near call factory.shardnet.near create_staking_pool ‘{“staking_pool_id”: “<pool id>”, “owner_id”: “<accountId>”, “stake_public_key”: “<public key>”, “reward_fee_fraction”: {“numerator”: 5, “denominator”: 100}, “code_hash”:”DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ”}’ — accountId=”<accountId>” — amount=30 — gas=300000000000000

From the example above, you need to replace:

Pool ID: Staking pool name, the factory automatically adds its name to this parameter, creating {pool_id}.{staking_pool_factory} Examples:
If pool id is stakewars will create : stakewars.factory.shardnet.near
Owner ID: The SHARDNET account (i.e. stakewares.shardnet.near) that will manage the staking pool.
Public Key: The public key in your validator_key.json file.
5: The fee the pool will charge (e.g. in this case 5 over 100 is 5% of fees).
Account Id: The SHARDNET account deploying and signing the mount tx. Usually the same as the Owner ID.
Now check in the explore: https://explorer.shardnet.near.org/nodes/validators

![29](https://user-images.githubusercontent.com/108926478/180350784-256da870-9348-4c17-a341-63db3d18ab40.PNG)

Congratulation! you are successfully create a Node Validator

Now you can check out some transaction guides here: https://github.com/near/stakewars-iii/blob/main/challenges/003.md#transactions-guide

Other functions that can be used:

# Ping

near call <staking_pool_id> ping ‘{}’ — accountId <accountId> — gas=300000000000000

# Balances Total Balance Command:

near view <staking_pool_id> get_account_total_balance ‘{“account_id”: “<accountId>”}’

# Staked Balance

near view <staking_pool_id> get_account_staked_balance ‘{“account_id”: “<accountId>”}’

# Unstaked Balance

near view <staking_pool_id> get_account_unstaked_balance ‘{“account_id”: “<accountId>”}’

# Available for Withdrawal

near view <staking_pool_id> is_account_unstaked_balance_available ‘{“account_id”: “<accountId>”}’

# Pause / Resume Staking

near call <staking_pool_id> pause_staking ‘{}’ — accountId <accountId>

# Resume

near call <staking_pool_id> resume_staking ‘{}’ — accountId <accountId>

You have now configured your Staking pool:

https://explorer.shardnet.near.org/nodes/validators

IV:Challenge 004.md:

Setup tools for monitoring node status.

We have setup log in challenge 002

Use this command to see log:

journalctl -n 100 -f -u neard | ccze -A

Now we install RPC with this commandsudo apt install curl jq:

sudo apt install curl jq

Common Commands:
####### Check your node version: Command:

curl -s http://127.0.0.1:3030/status | jq .version

####### Check Delegators and Stake Command:

near view <your pool>.factory.shardnet.near get_accounts '{"from_index": 0, "limit": 10}' --accountId <accountId>.shardnet.near
####### Check Reason Validator Kicked Command:

curl -s -d '{"jsonrpc": "2.0", "method": "validators", "id": "dontcare", "params": [null]}' -H 'Content-Type: application/json' 127.0.0.1:3030 | jq -c '.result.prev_epoch_kickout[] | select(.account_id | contains ("<POOL_ID>"))' | jq .reason
####### Check Blocks Produced / Expected Command:

curl -s -d '{"jsonrpc": "2.0", "method": "validators", "id": "dontcare", "params": [null]}' -H 'Content-Type: application/json' 127.0.0.1:3030 | jq -c '.result.current_validators[] | select(.account_id | contains ("POOL_ID"))'

V:Challenge 005.md:

Deliverables
Article doing a step-by-step guide on how to mount a node validator. (GitHub or Medium)
Submit the form !(https://docs.google.com/forms/d/e/1FAIpQLScp9JEtpk1Fe2P9XMaS9Gl6kl9gcGVEp3A5vPdEgxkHx3ABjg/viewform) with your article.

VI:Challenge 006.md:

### Create Crontab for the server

**Create a new scripts folder:**

Create a new file on /home/<USER_ID>/scripts/ping.sh

#!/bin/sh
# Ping call to renew Proposal added to crontab

export NEAR_ENV=shardnet
export LOGS=/home/<USER_ID>/logs
export POOLID=<YOUR_POOL_ID>
export ACCOUNTID=<YOUR_ACCOUNT_ID>

echo "---" >> $LOGS/all.log
date >> $LOGS/all.log
near call $POOLID.factory.shardnet.near ping '{}' --accountId $ACCOUNTID.shardnet.near --gas=300000000000000 >> $LOGS/all.log
near proposals | grep $POOLID >> $LOGS/all.log
near validators current | grep $POOLID >> $LOGS/all.log
near validators next | grep $POOLID >> $LOGS/all.log

Create a new crontab, running every 5 minutes:

crontab -e
*/5 * * * * sh /home/<USER_ID>/scripts/ping.sh
List crontab to see it is running:

crontab -l
Review your logs

cat home/<USER_ID>/logs/all.log

Ping is done periodically to network. (Every 5 minutes)
