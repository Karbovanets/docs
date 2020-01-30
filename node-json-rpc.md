# Karbo Node JSON RPC API

The daemon JSON RPC is a HTTP server which provides JSON 2.0 RPC interface for interacting with a daemon and a block explorer.

To start Daemon JSON RPC API server you should specify a port on which server binds (additionally to standard daemon's arguments). You can choose any free port. To do that execute the following command from the command line:
```
 karbowanecd --rpc-bind-port=32348 
```
If you want Daemon to be accessed from other computer not only yours you should also use a `--rpc-bind-ip 0.0.0.0` command. To do that execute the following command from the command line:
```
 karbowanecd --rpc-bind-ip=0.0.0.0 --rpc-bind-port=32348 
```
Having done that you're ready to operate with the daemon through the following API URLs (e.g., your IP address is 126.0.1.100):
```
 http://126.0.1.100:32348/json_rpc
 http://localhost:32348/json_rpc
```

To make a JSON RPC request to your Daemon RPC you should use a POST request that looks like this:

`http://<service address>:<service port>/json_rpc`

Parameter            | Description
-------------------- | -------------------------------------------------------------
`<service address>`  | IP of Daemon RPC, if it is located on local machine it is either 127.0.0.1 or localhost
`<service port>`     | Daemon RPC port, by default it is bound to 32348 port, but it can be manually bound to any port you want




## Available commands

### getblockcount

`getblockcount()` method returns the current chain height.

No Input.

**Output**

Argument         | Description          | Format
---------------- | -------------------- | ------
count            | Current chain height | int
status           | Status of request    | string


### getblockhash

`getblockhash()` method returns block hash by its height.

**Input**

Argument        | Mandatory     | Description           | Format
--------------- | ------------- | --------------------- | ------
height          | Yes           | The height of the block whose previous hash is to be retrieved. | int

**Output**

Argument         | Description          | Format
---------------- | -------------------- | ------
result           | Hash of previous block | int


### getblocktemplate

`getblocktemplate(reserve_size, addr)` method returns blocktemplate with an empty "hole" for nonce.

**Input**

Argument | Mandatory | Description  | Format
-------- | --------- | ------------ | ------
reserve_size | Yes | Size of the reserve to be specified | int
wallet_address | Yes | Valid TurtleCoin wallet address | String

**Output**

Argument | Description | Format
-------- | ---------- | ------
blocktempate_blob | Blocktemplate with empty "hole" for nonce | string
difficulty | Difficulty of the network | int
height | Chain height of the network | int
reserved_offset | Offset reserved | int
status | Status of the network | string


### submitblock

`submitblock(block_blob)` method submits mined block.

**Input**

Argument | Mandatory | Description | Format
-------- | --------- | ----------- | ------
block_blob | Yes | Block blob of the mined block | string

**Output**

Argument         | Description          | Format
---------------- | -------------------- | ------
status           | Status of request    | string


### getlastblockheader

`getlastblockheader` method returns the last block header.

No Input

**Output**

Argument | Description | Format
------- | ---------- | --------
block_size | size of the block | int
depth | height away from the known top block | int
difficulty | difficulty of the last block | int
hash | hash of the last block | string
height | height of the last block | int
major_version | - | int
minor_version | - | int
nonce | - | int
num_txs | Number of transactions in the block | int
orphan_status | whether the last block was an orphan or not | bool
prev_hash | hash of the previous block | string
reward | reward of the block | str
timestamp | the time at which the block is occured on chain since Unix epoch | int
status | status of the request | string


### getblockheaderbyhash

`getblockheaderbyhash()` returns block header by given block hash.

**Input**

Argument | Mandatory | Description | Format
-------- | ---------- | ----------- | -----
hash | Yes   | Hash of the block | string

**Output**

Argument | Description | Format
------- | ---------- | --------
block_size | size of the block | int
depth | height away from the known top block | int
difficulty | difficulty of the requested block | int
hash | hash of the requested block | string
height | height of the requested block | int
major_version | - | int
minor_version | - | int
nonce | - | int
num_txs | Number of transactions in the block | int
orphan_status | whether the requested block was an orphan or not | bool
prev_hash | hash of the previous block | string
reward | reward of the block | str
timestamp | the time at which the block is occured on chain since Unix epoch | int
status | status of the request | string


### getblockheaderbyheight

`getblockheaderbyheight()` method returns block header by given block height

**Input**

Argument | Mandatory | Description | Format
------ | ----------- | ----------- | -----
height | Yes   | Height of the block | int

**Output**

Argument | Description | Format
------- | ---------- | --------
block_size | size of the block | int
depth | height away from the known top block | int
difficulty | difficulty of the requested block | int
hash | hash of the requested block | string
height | height of the requested block | int
major_version | - | int
minor_version | - | int
nonce | - | int
num_txs | Number of transactions in the block | int
orphan_status | whether the requested block was an orphan or not | bool
prev_hash | hash of the previous block | string
reward | reward of the block | str
timestamp | the time at which the block is occured on chain since Unix epoch | int
status | status of the request | string


### getblockbyheight

`getblockbyheight()` method returns information on a single block by height.

**Input**

Argument        | Mandatory     | Description           | Format
--------------- | ------------- | --------------------- | ------
blockHeight     | Yes           | height of the block   | int

**Output**

Argument | Description | Format
------- | ---------- | --------
alreadyGeneratedCoins | total number of coins generated in the network upto that block | string
alreadyGeneratedTransactions | total number of transactions present in the network upto that block | int
baseReward | calculated reward | int
blockSize | size of the block | int
cumulativeDifficulty | cumulative difficulty is the sum of all block's difficulties up to this block including | int
depth | height away from the known top block | int
difficulty | difficulty of the requested block | int
effectiveSizeMedian | fixed constant for max size of block | int
hash | hash of the requested block | string
index | index of the requested block | int
isOrphaned | whether the requested block was an orphan or not | bool
majorVersion | - | int
minorVersion | - | int
nonce | - | int
penalty | penalty in block reward determined for deviation | float
prevBlockHash | hash of the previous block | string
reward | total reward of the block after removing penalty | str
sizeMedian | calculated median size from last 100 blocks | int
timestamp | the time at which the block is occured on chain since Unix epoch | int
totalFeeAmount | total fees for the transactions in the block | int
transactions | Array of transactions in the block | array
transactionsCumulativeSize | total sum of size of all transactions in the block | int
status | status of the request | string

Transaction Attributes: see [gettransaction](#gettransaction)


### getblockbyhash

`getblockbyhash()` method returns information on a single block by its hash.

**Input**

Argument        | Mandatory     | Description           | Format
--------------- | ------------- | --------------------- | ------
hash            | Yes           | hash of the block     | string

**Output**

see [getblockbyheight](#getblockbyheight)


### getblocksbyheights

`getblocksbyheights()` method returns information on a vector of blocks by their heights.

**Input**

Argument        | Mandatory     | Description           | Format
--------------- | ------------- | --------------------- | ------
blockHeights    | Yes           | vector of heights of the blocks | int

**Output**

Argument | Description | Format
------- | ---------- | --------
blocks | vector of block details where each block has the same output format as single block details in [getblockbyheight](#getblockbyheight) or [getblockbyhash](#getblockbyhash) methods | -
status | status of the request | string


### getblocksbyhashes

`getblocksbyhashes()` method returns information on a vector of blocks by their hashes.

**Input**

Argument        | Mandatory     | Description           | Format
--------------- | ------------- | --------------------- | ------
blockHashes     | Yes           | vector of hashes of the blocks | string

**Output**

Argument | Description | Format
------- | ---------- | --------
blocks | vector of block details where each block has the same output format as single block details in [getblockbyheight](#getblockbyheight) or [getblockbyhash](#getblockbyhash) methods | -
status | status of the request | string




### getcurrencyid

`getcurrencyid()` method returns unique currency identifier.

No Input

**Output**

Argument | Description | Format
-------- | ----------- | ------
currency_id_blob | unique currency identifier | string



## Examples

### getblockcount

Input:
```
{
	"jsonrpc": "2.0",
	"id": "test",
	"method": "getblockcount",
	"params": {}
}
```
Output: 
```
 {
 	"id": "test",
 	"jsonrpc": "2.0",
 	"result": {
 		"count": 123456,
 		"status": "OK"
 	}
 }
```
### getblockhash

Input:
```
 {
 	"jsonrpc": "2.0",
 	"id": "test",
 	"method": "getblockhash",
 	"params": {
 		"height": 123456
 	}
 }
```
Output:
```
 {
 	"id": "test",
 	"jsonrpc": "2.0",
 	"result": "a7428..."
 }
```
### getblocktemplate

Input:
```
 {
 	"jsonrpc": "2.0",
 	"id" : "test",
 	"method": "getblocktemplate",
 	"params": {
 		"reserve_size": 200,
 		"wallet_address": "28j5g2Hbe1..."
 	}
 }
```
Output:
```
 {
 	"id": "test",
 	"jsonrpc": "2.0",
 	"result": {
 		"blocktemplate_blob": "0100de...",
 		"difficulty": 65563,
 		"height": 123456,
 		"reserved_offset": 395,
 		"status": ""
 	}
 }
```
### submitblock

Input: 
```
 {
 	"jsonrpc": "2.0",
 	"id" : "test",
 	"method": "submitblock",
 	"params": ["0100b...."]
 }
```
Output:
```
 {
 	"id": "test",
 	"jsonrpc": "2.0",
 	"result": {
 		"status" : "OK"
 	}
 }
```
### getlastblockheader

Input:
```
 {
 	"jsonrpc": "2.0",
 	"id" : "test",
 	"method": "getlastblockheader"
 }
```
Output:
```
 {
 	"id": "test",
 	"jsonrpc": "2.0",
 	"result": {
 		"block_header": {
 			"depth": 1,
 			"difficulty": 65198,
 			"hash": "9a8be83...",
 			"height": 123456,
 			"major_version": 1,
 			"minor_version": 0,
 			"nonce": 2358499061,
 			"orphan_status": false,
 			"prev_hash": "dde56b7e...",
 			"reward": 44090506423186,
 			"timestamp": 1356589561
 		},
 		"status": "OK"
 	}
 }
```
### getblockheaderbyhash

Input:
```
 {
 	"jsonrpc": "2.0",
 	"id" : "test",
 	"method": "getblockheaderbyhash",
 	"params": {
 		"hash" : "9a8be8..."
 	}
 }
```
Output:
```
 {
 	"id": "test",
 	"jsonrpc": "2.0",
 	"result": {
 		"block_header": {
 			"depth": 1,
 			"difficulty": 65198,
 			"hash": "9a8be83...",
 			"height": 123456,
 			"major_version": 1,
 			"minor_version": 0,
 			"nonce": 2358499061,
 			"orphan_status": false,
 			"prev_hash": "dde56b7e...",
 			"reward": 44090506423186,
  			"timestamp": 1356589561
 		},
 		"status": "OK"
 	}
 }
```
### getblockheaderbyheight

Input:
```
 {
 	"jsonrpc": "2.0",
 	"id" : "test",
 	"method": "getblockheaderbyheight",
 	"params": {
 		"height" : 123456
 	}
 }
```
Output:
```
 {
 	"id": "test",
 	"jsonrpc": "2.0",
 	"result": {
 		"block_header": {
 			"depth": 1,
 			"difficulty": 65198,
  			"hash": "9a8be83...",
 			"height": 123456,
 			"major_version": 1,
 			"minor_version": 0,
 			"nonce": 2358499061,
 			"orphan_status": false,
 			"prev_hash": "dde56b7e...",
 			"reward": 44090506423186,
 			"timestamp": 1356589561
 			},
 		"status": "OK"
 	}
 }
```

### getblockbyheight

Input:
```
{
  "jsonrpc": "2.0",
  "method": "getblockbyheight",
  "id": "test",
  "params": {
	"blockHeight": 399666 
  }
}
```
Output:
```
{
   "id":"test",
   "jsonrpc":"2.0",
   "result":{
      "block":{
         "alreadyGeneratedCoins":7822291504630269000,
         "alreadyGeneratedTransactions":842837,
         "baseReward":8307330332565,
         "blockSize":23716,
         "cumulativeDifficulty":2277860049927920,
         "depth":5,
         "difficulty":14377384679,
         "effectiveSizeMedian":1000000,
         "hash":"4cc94394440e64461766d0e7c675498da934d70a63b143606246f0e6e26d1bde",
         "index":399666,
         "isOrphaned":false,
         "majorVersion":4,
         "minorVersion":0,
         "nonce":3653353692,
         "penalty":0,
         "prevBlockHash":"72199371e92ee3dd95f0993f49a82d3dc7b7175dc004ad9c4437167a7138bd13",
         "reward":8507330332565,
         "sizeMedian":532,
         "timestamp":1568118204,
         "totalFeeAmount":200000000000,
         "transactions":[
            {
               "blockHash":"4cc94394440e64461766d0e7c675498da934d70a63b143606246f0e6e26d1bde",
               "blockIndex":399666,
               "extra":{
                  ...
               },
               "fee":0,
               "hash":"33688742d5e0e84da4cd195d9b6970ce539590b152d6e9095d6837f26defcf74",
               "inBlockchain":true,
               "inputs":[

               ],
               "mixin":0,
               "outputs":[

               ],
               "paymentId":"0000000000000000000000000000000000000000000000000000000000000000",
               "signatures":[
                  ...
               ],
               "signaturesSize":0,
               "size":500,
               "timestamp":1568118204,
               "totalInputsAmount":0,
               "totalOutputsAmount":8507330332565,
               "unlockTime":399676
            },
            {
               ...
            }
         ],
         "transactionsCumulativeSize":23640
      },
      "status":"OK"
   }
}
```

### getblockbyhash

Input:
```
{
  "jsonrpc": "2.0",
  "method": "getblockbyhash",
  "id": "test",
  "params": {
	"hash": "4cc94394440e64461766d0e7c675498da934d70a63b143606246f0e6e26d1bde" 
  }
}
```
Output:
```
{
   "id":"test",
   "jsonrpc":"2.0",
   "result":{
      "block":{
         "alreadyGeneratedCoins":7822291504630269000,
         "alreadyGeneratedTransactions":842837,
         "baseReward":8307330332565,
         "blockSize":23716,
         "cumulativeDifficulty":2277860049927920,
         "depth":6,
         "difficulty":14377384679,
         "effectiveSizeMedian":1000000,
         "hash":"4cc94394440e64461766d0e7c675498da934d70a63b143606246f0e6e26d1bde",
         "index":399666,
         "isOrphaned":false,
         "majorVersion":4,
         "minorVersion":0,
         "nonce":3653353692,
         "penalty":0,
         "prevBlockHash":"72199371e92ee3dd95f0993f49a82d3dc7b7175dc004ad9c4437167a7138bd13",
         "reward":8507330332565,
         "sizeMedian":532,
         "timestamp":1568118204,
         "totalFeeAmount":200000000000,
         "transactions":[
            {
               ...
            },
            {
               ...
            }
         ],
         "transactionsCumulativeSize":23640
      },
      "status":"OK"
   }
}
```

### getblocksbyheights

Input:
```
{
  "jsonrpc": "2.0",
  "method": "getblocksbyheights",
  "id": "test",
  "params": {
	"blockHeights": [399666, 399667] 
  }
}
```
Output:
```
{
   "id":"test",
   "jsonrpc":"2.0",
   "result":{
      "blocks":[
         {
            "alreadyGeneratedCoins":7822291504630269000,
            "alreadyGeneratedTransactions":842837,
            "baseReward":8307330332565,
            "blockSize":23716,
            "cumulativeDifficulty":2277860049927920,
            "depth":6,
            "difficulty":14377384679,
            "effectiveSizeMedian":1000000,
            "hash":"4cc94394440e64461766d0e7c675498da934d70a63b143606246f0e6e26d1bde",
            "index":399666,
            "isOrphaned":false,
            "majorVersion":4,
            "minorVersion":0,
            "nonce":3653353692,
            "penalty":0,
            "prevBlockHash":"72199371e92ee3dd95f0993f49a82d3dc7b7175dc004ad9c4437167a7138bd13",
            "reward":8507330332565,
            "sizeMedian":532,
            "timestamp":1568118204,
            "totalFeeAmount":200000000000,
            "transactions":[ ... ],
            "transactionsCumulativeSize":23640
         },
         {
            ...
         }
      ],
      "status":"OK"
   }
}
```

### getblocksbyhashes

Input:
```
{
  "jsonrpc": "2.0",
  "method": "getblocksbyhashes",
  "id": "test",
  "params": {
	"blockHashes": [
    	"4cc94394440e64461766d0e7c675498da934d70a63b143606246f0e6e26d1bde",
        "72199371e92ee3dd95f0993f49a82d3dc7b7175dc004ad9c4437167a7138bd13"
     ] 
  }
}
```
Output:
```
{
   "id":"test",
   "jsonrpc":"2.0",
   "result":{
      "blocks":[
         {
            "alreadyGeneratedCoins":7822291504630269000,
            "alreadyGeneratedTransactions":842837,
            "baseReward":8307330332565,
            "blockSize":23716,
            "cumulativeDifficulty":2277860049927920,
            "depth":11,
            "difficulty":14377384679,
            "effectiveSizeMedian":1000000,
            "hash":"4cc94394440e64461766d0e7c675498da934d70a63b143606246f0e6e26d1bde",
            "index":399666,
            "isOrphaned":false,
            "majorVersion":4,
            "minorVersion":0,
            "nonce":3653353692,
            "penalty":0,
            "prevBlockHash":"72199371e92ee3dd95f0993f49a82d3dc7b7175dc004ad9c4437167a7138bd13",
            "reward":8507330332565,
            "sizeMedian":532,
            "timestamp":1568118204,
            "totalFeeAmount":200000000000,
            "transactions":[ ... ],
            "transactionsCumulativeSize":23640
         },
         {
            ...
         }
      ],
      "status":"OK"
   }
}
```




### getcurrencyId

Input:
```
 {
 	"jsonrpc": "2.0",
 	"id" : "test",
 	"method": "getcurrencyid"
 }
```
Output:
```
 {
 	"id": "test",
 	"jsonrpc": "2.0",
 	"result": {
 		"currency_id_blob": "3125b79e4a42f8d4d2fc4dffea8442e185ebda940ecd4d3b449056a4ea0efea4"
 	}
 }
```