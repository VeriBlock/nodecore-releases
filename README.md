
NOTE: The direct link to the zip file containing the entire NodeCore Suite is here (under github releases): https://github.com/VeriBlock/nodecore-releases/releases/download/v0.1.1/nodecore-all-testnet-0.1.1.zip


# Overview 

General links:

* Block Explorer for TestNet: https://TestNet.Explore.Veriblock.org
* Submit any technical issues to github: https://github.com/VeriBlock/nodecore-releases/issues
* Home page: https://www.veriblock.org
* Wiki: https://wiki.veriblock.org

VeriBlock Proof-of-Proof has 4 components. Each of these will run in their own command window.

* nodecore-*.zip - Backend NodeCore instance. 
* nodecore-reference-pow-*.zip - Proof-of-Work miner to add next nodecore block
* nodecore-pop-*.zip - Proof-of-Proof mining
* nodecore-cli-*.zip - Command Line. Use this to send transactions.

First step is to run a local instance of NodeCore. Whether you mine or use the command line, you'll need a local instance running. For example the command line connects to your local instance, and that local instance connects to the entire network.

# Get each part running 

First, ensure that Java is running. Install Java 1.8 from here: https://java.com/en/download/manual.jsp.

Caution: If you use Windows, and Windows explorer hides "known file extensions," then make sure you are using the correct files (i.e. "Nodecore.bat" and "NodeCore" will both show as "NodeCore"). For this readme, it will be much easier if you know the file extension of every file you're working with. The icon of the correct (.bat) file should look like two gears in a box.

## How to run NodeCore 

1. Unzip the nodecore-*.zip file
2. In the bin folder, if Windows then run nodecore.bat, if linux then run nodecore

Note: On linux systems, you may need to make the nodecore shell script executable by running the following command:

```
chmod a+x nodecore
```

When you first run NodeCore, it will create several other log files in the bin folder (nodecore.properties, veriblock.nodecore.log, nodecore.dat, etc...), and load the existing blockchain. 

NodeCore may take several minutes to load all the blocks in the blockchain. See the highest block at https://TestNet.Explore.Veriblock.org. This shows the number of blocks your local instance must load. NodeCore will create a cache file such that when you restart it they will load faster next time.

## How to run the Command Line 

**Note:** If you are having trouble running nodecore-cli on linux, you may need to make nodecore-cli executable:
```
chmod a+x nodecore-cli
```

1. Ensure that nodecore is running (see previous step)
2. Unzip nodecore-cli-*.zip
3. In the bin folder, if Windows then run nodecore-cli.bat, if linux then run nodecore-cli
4. Connect to the local instance by running this command "connect 127.0.0.1:10500". You should see "200 Success".
5. Type "help" to see all available commands. You should see a list of many commands, such as "getinfo"
6. Type "getinfo". You should see data back such as:


```
rpc (127.0.0.1:10500) > {
  "payload": {
    "default_address": {
      "address": "V6RRxmzJAhLkeWTzcFzQkQEgP2hC1e",
      "amount": 0
    },
    "estimated_hash_rate": 56232,
    "number_of_blocks": 104,
    "transaction_fee": 1,
    "last_block": {
      "pow_coinbase_reward": 35000000000,
      "pop_coinbase_reward": 0,
      "transaction_fees": 1,
      "size": 62,
      "number": 103,
      "timestamp": 1520466056,
      "hash": "000000F4FCE491047796B5EFBEAE482787FF948152D11CB7",
      "previous_hash": "0000006FC1D6387C3DEDFD2B4EB9DEC788621F53705797BB",
      "difficulty": 51331648,
      "winning_nonce": 762757820,
      "ledger_hash": "FAF249E56914265BFCF5D02850F41AE086CE0D9FF89531B0"
    },
    "difficulty": 1000000
  },
  "success": true,
  "messages": []
}
```


## How to run the PoW Miner 

The PoW Miner helps get the next block added to the VeriBlock blockchain. It will connect to a local instance of NodeCore, using UCP on port 8501.

**Note: **If you are having trouble running nodecore-reference-pow on linux, you may need to make nodecore-reference-pow executable:
chmod a+x nodecore-reference-pow

1. Ensure that nodecore is running
2. In the NodeCore CLI, run the "startpool" command. This will start the UCP NodeCore protocol on port 8501, which the miner needs.
3. Unzip nodecore-reference-pow.zip
4. In the bin folder, if Windows then run nodecore-reference-pow.bat, if linux then run nodecore-reference-pow
5. Enter the input arguments
 1. How many threads would you like to mine on? --> such as 2 or 8.
 2. What host:port would you like to connect to for mining? --> 127.0.0.1:8501
 3. What address would you like to mine to? --> the default address for your local instance of nodecore, such as "V6RRxmzJAhLkeWTzcFzQkQEgP2hC1e". Run getinfo in the commandline to see the default address.

## How to run the PoP Miner 

**Prerequisites:**

See this Bitcoin page for background info: [https://en.bitcoin.it/wiki/Running_Bitcoin](https://en.bitcoin.it/wiki/Running_Bitcoin)

1. Download Bitcoin Core https://bitcoin.org/en/download, run Bitcoin in testnet mode, and allow it to fully sync. This may take a while depending on your network connection.
2. Run bitcoin TestNet by passing in the testnet parameter:
 1. Windows: bitcoin-qt.exe -testnet
 2. Linux: bitcoind -testnet
3. Set up a rpc user and password in the bitcoin.conf file
 1. In Bitcoin Core, goto: Settings > Options > Main (tab) > Open Config File (button).
 2. If prompted with "The configuration file is used to...", then click ok.
 3. bitcoin.conf (a plaintext file) will open.
 4. specify the flags like below (server=1, rpcuser=your_username, rpcpassword=your_password), and save the file. Re-click the "Open Config File" to ensure the settings did indeed save (they should have)

```
server=1
rpcuser=bitcoinrpc
rpcpassword=someTestNetPassword123
```


Get Bitcoin on the testnet from a faucet. Running PoP requires a small amount of Bitcoin. We do not want to endorse a specific faucet, but you can see a list here: https://en.bitcoin.it/wiki/Testnet#Faucets. Get a new Bitcoin testnet address from your running instance of Bitcoin, and then enter it into one of the testnet sites to receive testnet Bitcoin.


**Run the PoP Miner**

**Note: **If you are having trouble running nodecore-reference-pow on linux, you may need to make nodecore-reference-pow executable:
chmod a+x nodecore-pop

1. Run a local instance of NodeCore
2. Unzip nodecore-pop-*.zip
3. In the bin folder, if Windows then run nodecore-pop.bat, if linux then run nodecore-pop
4. You will be prompted for a series of questions. Below is sample inputs. Note that Bitcoin TestNet port is 18332 (not 18333).

```
Please enter the VeriBlock NodeCore host [Default: 127.0.0.1](]):
 > 127.0.0.1
Please enter the VeriBlock NodeCore port [10500](Default:):
 > 10500
Please enter the Bitcoin RPC host [127.0.0.1](Default:):
 > 127.0.0.1
Please enter the Bitcoin RPC port [8332](Default:):
 > 18332
Please enter a funded Bitcoin address you would like to use for PoP:
 > mwAY47kNhN2TY1nc23Y18aDi4botjpGzAy
Please enter your Bitcoin RPC username:
 > bitcoinrpc
Please enter your Bitcoin RPC password:
 > someTestNetPassword123
How many BTC would you like to pay as a transaction fee for each PoP? (Suggested: 0.001)
 > 0.001
```

Note that after entering this info once, it will be saved to a ncpop.properties file for future reference. If you ever need to change these entries in the future, you can either delete ncpop.properties and restart nodecore-pop (where it will prompt you for new entries), or you can change the entires in the configuration file directly.

Because PoP Mining costs a small amount of BTC, you will be prompted for each transaction with something like: "Press enter to pay 0.001 BTC to perform a PoP! (q to quit)"

If the PoP Miner appears frozen, hit "ENTER" to proceed.

Go back to your Bitcoin Core, Transactions tab, and you will see PoP Transactions. Drill down on a transaction and you'll see a transaction ID. After a few minutes, this transaction ID should show up on testnet blockexplorers, such as http://testnet.coinsecrets.org.

```
Status: 0/unconfirmed, in memory pool
Date: 3/9/2018 14:33
Debit: 0.00000000 BTC
Transaction fee: -0.00100000 BTC
Net amount: -0.00100000 BTC
Transaction ID: 52bac8bad5c9d71f1adcf166c5ef5e651f269851b1816b61cb99ed62268f512b
Transaction total size: 283 bytes
Output index: 0
```

Drill down on the block explorer, and you will see the proof in the OP_RETURN. Ignore the first 4 characters (0x4c refers to the OP_PUSHDATA1 opcode, and 0x50 refers to 80 bytes [the size of our published data] being pushed onto the stack), look at the last 160 (80 bytes), and that is your proof on the BTC testnet!

```
OP_RETURN
4c5000000001000000f29717032fb910956d001e9ae5554540864b4c998cf7233ca3ff78109365086b0e7ad55c480ce9dd55fa6763275aa2eedc0319ca1c0ed60f1df7918c1b4232bfdc584dfdbaa50ae224
```

# Common Use Cases 

## Send transactions across the network  

Using the Command Line, you can send transactions from one address to another. Note that you must already have VeriBlock coins in your address, which you can acquire by PoW mining.

1. Open the Command Line and connect it to a local instance of NodeCore
2. run the send command, targeting an address to send TO (the command will be smart enough to pick an address that has sufficient funds) 
3. run: send 10 VE2TkS4er4JeZJRnPkSKUdSeaAew5E
4. It will take several minutes for the transaction to get approved by PoW miners and propagated across the network to other nodecore instances
5. in the meantime, run these command lines to see that transaction: 
 1. getpendingtransactions
 2. gethistory
6. Check the transaction on the website: https://testnet.explore.veriblock.org

Running gethistory will show a snippet like:
```
"type": "signed",
"signed": {
	"signature": "304502200FC3D7106A824CCD9B2E6217EA5D33CD817A4CBE81B1C8EEF8B4998816130F9A022100C1823209EABA935149D521646BF543B45F9325C5547B4B44B93CD0B47D31E718",
	"public_key": "3056301006072A8648CE3D020106052B8104000A034200040A8B7724ED7892A1BC722CB140971A6A154E95F7605EC0E941C27CEFA9D477D6D8E94E1660CDBC030F3F9297C0221E80C3DF4E328CCC0B9277CEAB095EF03909",
	"signature_index": 1,
	"transaction": {
	  "size": 60,
	  "txid": "4E5EB2B9CD7C19C0D859E62DC6FD302E3F1BCB9B89E6F2484F58D3785470FC10",
	  "data": "",
	  "type": "standard",
	  "fee": "0.00000001",
	  "timestamp": 1521399261,
	  "source_amount": "10.00000000",
	  "merkle_path": "",
	  "source_address": "V8geBiWHFHCLCf3K2EjtBq3SyDyDh6",
	  "bitcoin_transaction": "N/A",
	  "bitcoin_block_header_of_proof": "N/A",
	  "endorsed_block_header": "N/A",
	  "context_bitcoin_block_headers": [
		"N/A"
	  ],
	  "outputs": [
		{
		  "address": "V7ePN8RRX4ULYuGdec7QWnQbqDx6gQ",
		  "amount": "9.99999999"
		}
	  ]
	}
}
```

## Add new blocks to the blockchain (Proof-of-Work Mining) 

1. Run the PoW Miner per instructions above (start local nodecore, open the command line, run startpool, etc...)
2. You are mining! As users submit transactions, you'll help add those transactions to the blockchain by including them in your next block (and collecting the transaction fees for doing so)

## Secure VeriBlock to Bitcoin (Proof-of-Proof Mining) 

1. Run the PoP Miner per instructions above
2. You are PoP Mining!

# How to see what's happening 

## Command Line 

The command line uses the public API from NodeCore.

Some of the especially useful commands are:

help: Provides a list of all the commands. Run "help <command>" for more details.

getbalance: Returns the balance for a given address (or all addresses if none is specified)

getinfo: Returns general information about this node and the presently-known blockchain

getpeerinfo: Returns a list of connected peers

startpool: Starts the built-in pool service in NodeCore

## VeriBlock Explorer website 

The VeriBlock explorer shows the block and transaction details on the VeriBlock blockchain. If you make a transaction, it should show up here.

https://testnet.explore.veriblock.org

## Bitcoin Explorer 

The BTC testnet explorer shows the block and transaction details for BTC testnet. When running Proof-of-Proof transactions, the proof will show up in the OP_RETURN code on Bitcoin (i.e. VeriBlock secures to Bitcoin)

Here is one such testnet explorer:

http://testnet.coinsecrets.org/

# FAQ 

## Where do I get coins to test with? 

* Run the PoW Miner and get block rewards
* Send a message to the public community channels, and someone can send you test coins

# Troubleshooting 

## PoW Miner won't start 

Ensure that you ran startpool on NodeCore (using the Command Line)

Ensure that you have a local instance of NodeCore already running

## PoP Miner appears frozen 

The PoP Miner is interactive. A PoP transaction requires a small amount of BTC, so before paying it prompts you to hit "ENTER". The system may appear frozen until you hit ENTER to pay the next transaction.

## Commandline getinfo returns error 

Ensure that the connected NodeCore instance is fully caught up, else it will return an error like:

```
rpc (127.0.0.1:10500) > ERROR: [V800] Remote service call failure io.grpc.StatusRuntimeException: UNAVAILABLE
```

## My local instance is added as its own peer

Modify the nodecore.properties file (in nodecore\bin) and add the key "peer.publish.address" with your IPv4 value. Get this value from a site like https://www.whatismyip.com

```
#peer.publish.address=73.92.111.111
peer.publish.address=<your_public_IP>
```

## One of the apps is frozen 

If this is Windows, clicking on the console scrollbar may freeze the application. Hit enter to continue running.



