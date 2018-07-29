
NOTE: The direct link to the zip file containing the entire NodeCore Suite is here (under github releases): https://github.com/VeriBlock/nodecore-releases/releases/download/v0.2.6/veriblock-nodecore-all-0.2.6.zip

The direct link to the GPU miner is: https://github.com/VeriBlock/nodecore-releases/releases/download/v0.2.1/veriblock-nodecore-pow-cuda-0.2.2-3-neuter32.zip

# Change log

##  0.2.0

Full new release

##  0.1.7

### NodeCore
* Stability fixes
* Add GRPC command getStateInfo to return state of nodecore

### NodeCore CommandLine
* Fix cosmetic issues with newline

### PoP Miner
* Fix bug where miner must be restarted to clear the "not-ready" flag.

##  0.1.6

### NodeCore
* Many stability fixes
* Blockchain loads much faster

### PoW Miner
* Add properties file to set command-line input for automated startup

##  0.1.5

### NodeCore
* Stability fixes
* Improves NodeCore to better handle when Bitcoin Testnet gets an extreme number of blocks in a very short period of time.

### PoW Miner
* Minor enhancements

### NodeCore CommandLine
* Minor enhancements

### PoP Miner
* Minor enhancements



##  0.1.4

* Updated RPC Ports: TestNet = 10501, MainNet (once it launches) will be 10500. When connecting with the NC_CLI to testnet, now use 10501 instead of 10500!
* Updated P2P Ports: TestNet = 6501, MainNet (once it launches) will be 6500. If you copied your nodecore.properties file from a previous version, please update "peer.external.hosts" to 6501. If you did not copy the nodecore.properties file, then no action required.
* The send command now treats the configured fee as the FEE-PER-BYTE to account for the new possibility of a transaction being more than one size in bytes. Consider changing your transactions fees accordingly (NC_CLI has the settxfee command).

### PoW Miner
* Releasing new GPU Miner

### NodeCore CommandLine
* New command to show what blocks are protected by PoP: getProtectedChildren, getProtectingParents
* Add importwallet (related to backupwallet)
* Fix send bug - If A has 100 and B has 100, then you can send 150, therefore 1 Send command can have multiple transactions. This means send can return multiple transactions.

### PoP Miner
* Action timeout is now configurable
* Add Cron Schedule for mining

### Dashboard
* Pop Usability sections - Address page shows PoP rewards, Transaction Page shows related Bitcoin transactions, Block Detail page shows * PoP payouts
* Fix difficulty setting to show decoded value

### NodeCore
* Stability fixes

### Relevant documentation:
* https://wiki.veriblock.org/index.php?title=HowTo_run_PoP_Miner - updates to page
* https://wiki.veriblock.org/index.php?title=NodeCore_CommandLine - updates to page for new commands
* https://wiki.veriblock.org/index.php?title=HowTo_run_PoW_GPU_Miner - release of GPU miner
* https://wiki.veriblock.org/index.php?title=HowTo_run_PoW_CPU_Miner - moved the existing PoW miner to here
* https://wiki.veriblock.org/index.php?title=HowTo_run_PoW_Miner - now points to both CPU and GPU miners



##  0.1.3

### PoP Miner
* New PoP Miner with interactive command line. You no longer need to run a Bitcoin daemon to do Proof-of-Proof

### NodeCore
* Stability fixes

### NodeCore CommandLine
* On connect, provide immediate error if cannot connect to a valid endpoint
* New command to see PoP endorsements: getpopendorsementsinfo
* Add BTC transaction Id to gettransaction to better see PoP-BTC link

### Relevant new documentation:
https://wiki.veriblock.org/index.php?title=HowTo_run_PoP_Miner - complete rewrite for new miner
https://wiki.veriblock.org/index.php?title=PoP_Miner_CommandLine - Command line reference for PoP Miner
https://wiki.veriblock.org/index.php?title=PoP_Transaction_LifeCycle - overview of a PoP transaction from start to finish

##  0.1.2

### NodeCore
* Peer to peer network protocol overhauled (Breaking change)
* TLS support on Admin RPC
* RPC Password option
* Added robustness to mining pool operation (Breaking change)
* Backup wallet RPC endpoint added
* Fixed a case in which Bitcoin blockchain view was not rolled back when forked
* Introduced support for multiple networks

### CLI
* Removed "peer" commands
* Backup wallet command
* Added support for TLS
* Added support for password

### PoW
* ExtraNonce support added

### PoP
* Compatibility updates with Bitcoin 0.16.0
* Added support for SegWit transactions



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
4. Connect to the local instance by running this command "connect 127.0.0.1:10501". You should see "200 Success".
5. Type "help" to see all available commands. You should see a list of many commands, such as "getinfo"
6. Type "getinfo". You should see data back such as:


```
rpc (127.0.0.1:10501) > {
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

The PoP Miner was rewritten in 0.1.3. This wiki explains how to run it:

https://wiki.veriblock.org/index.php?title=HowTo_run_PoP_Miner

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
rpc (127.0.0.1:10501) > ERROR: [V800] Remote service call failure io.grpc.StatusRuntimeException: UNAVAILABLE
```

## My local instance is added as its own peer

Modify the nodecore.properties file (in nodecore\bin) and add the key "peer.publish.address" with your IPv4 value. Get this value from a site like https://www.whatismyip.com

```
#peer.publish.address=73.92.111.111
peer.publish.address=<your_public_IP>
```

## One of the apps is frozen 

If this is Windows, clicking on the console scrollbar may freeze the application. Hit enter to continue running.

