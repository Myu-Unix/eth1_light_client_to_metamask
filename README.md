# How to submit an Ethereum Tx through Metamask via Geth "light client"

![img](header.png)

This tutorial is intended to explain how to setup a local ETH1 light client using Geth and how to submit an Ethereum Tx to the mempool through it.

This has the benefit that you do not **fully**rely on third-party infrastructure (i.e Infura) to access the Ethereum mempool but your Light node is getting data from full nodes so a full node might be an even better option if you can spare the cash for a 1TB+ SSD.

PR welcomed and no warranty, use it at your own risk. Always DYOR.

#### Install Geth on Linux

Get the latest Geth from https://geth.ethereum.org/downloads/ , here we are using 1.9.25

    tar xzvf geth-linux-amd64-1.9.25-e7872729.tar.gz
    cd geth-linux-amd64-1.9.25-e7872729.tar.gz
    
#### Run it !

    ./geth --data-dir /mnt/eth_chain --syncmode "light" --http --http.port 5566 --http.api personal,web3,eth,net --http.corsdomain '*' --rpc --rpcaddr <REPLACE_BY_YOUR_LOCAL_IP>

You can of course replace the --data-dir argument by the location of your choice, currently the light client takes < 500 MB of space.

For this tutorial, I have used 192.168.1.15 as "local IP", I will use this value later on. Change it accordingly.

Let the blockchain sync, with the light client it's pretty fast (around 15 mins). You can see if it's synced if you only have "Imported new block headers" messages on the logs.

#### Metamask Setup

Open Metamask, click on the Network drop down which is at the very top, select "Custom RPC"

Set those values :

**Network Name** : pick_whatever_you_want

**New RPC URL** : http://REPLACE_BY_YOUR_LOCAL_IP:HTTP_PORT (e.g here : 192.168.1.15:5566)

**Chain ID** : 1

![img](rpc_setup_mm.png)

If all goes well, Metamask will allow it !

You can then try to send a Tx through it to see if it works ! If you are fast enough, you'll see that your Geth client received a transaction in its logs.

That's all folks, happy setup ! :)
