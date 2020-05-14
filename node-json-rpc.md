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


### gettransaction

`gettransaction()` method returns information on a single transaction by its hash.

**Input**

Argument        | Mandatory     | Description             | Format
--------------- | ------------- | ----------------------- | ------
hash            | Yes           | hash of the transaction | string

**Output**

Argument | Description | Format
------- | ---------- | --------
status | status of the request | string
transaction | details of the transaction | json object

Transaction attributes:

Argument | Description | Format
------- | ---------- | --------
blockHash | hash of block containing this transaction | string
blockIndex | index of block containing this transaction | int
extra | transaction extra which can be any information | json object
fee | total fees of the transaction | int
hash | hash of the transaction | string
inBlockchain | wherer thransaction is included in block | boolean
inputs | inputs of the transaction | json object
mixin | mixin of the transaction | int
outputs | outputs of the transaction | json object
paymentId | payment Id of the transaction | string
signatures | array of transaction signatures | array
signaturesSize | the size of the signatures array | int
size | total size of the transaction | int
timestamp | timestamp of the block that includes transaction | int
totalInputsAmount | total amount on input side of the transaction | int
totalOutputsAmount | total amount present in the transaction | int
unlockTime | delay in unlocking the amount | int

Extra attributes: 

Argument | Description | Format
------- | ---------- | --------
nonce |  | array
publicKey | the public key of the transaction | string
raw | raw transaction extra in hex | string
size | the size of transaction extra | int

Inputs attributes:

The array of inputs, each having these attributes:

Argument | Description | Format
------- | ---------- | --------
data | the input data | json object
type | the type of input, can be `02` for normal transaction, `ff` for coinbase transaction | hex

In the case of coinbase transaction there is only one input with such attributes of `data`:

Argument | Description | Format
------- | ---------- | --------
amount | the amount of input | int
input | the input with `height` attribute denotig the block height | int

Normal transaction input `data` attributes:

Argument | Description | Format
------- | ---------- | --------
input | the input | json object
mixin | mixin | int
outputs | correspoding ouptuts in transactions, the size of the array is equal to mixin size | array

`input` attributes:

Argument | Description | Format
------- | ---------- | --------
amount | the amount of the input, in atomic units | int
k_image | the key image for the given input | string
key_offsets | a list of integer offets to the input, these are the set of outputs used as "fake" outputs, as well as real | array 

`outputs` attributes:

Argument | Description | Format
------- | ---------- | --------
number | the number of output in transaction | int
transactionHash | the hash of the transaction containing this output for this input | string

Outputs attributes:

Argument | Description | Format
------- | ---------- | --------
globalIndex | global index for output | int
output | the output information | json object

`output` attributes:

Argument | Description | Format
------- | ---------- | --------
amount | the amount, in au | 
target | has `data` json object and `type` | json object 

`target` attributes:

Argument | Description | Format
------- | ---------- | --------
data | containing `key` string attribute to which output is sent | json object
type | the type of the output target | int

Signatures attributes:

each signature element has

Argument | Description | Format
------- | ---------- | --------
first | the number of signature which repeats as many times as transacion mixin count (signature for each input in mixin) | int
second | the signature | string


### gettransactionspool

`gettransactionspool()` method the list of short details of transactions present in mempool.

No Input

**Output**

Argument | Description | Format
------- | ---------- | --------
status | status of the request | string
transactions | array of transactions in mempool* | array

\* empty array means that currently there are no transactions in mempool

Transactions entry attributes:

Argument | Description | Format
------- | ---------- | --------
hash | the hash of transaction | string
fee | the network fee of transaction | int
amount_out | total amount in transaction | int
size | the size of transaction | int
receive_time | the timestamp when transaction was received by queried node | int


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




### gettransaction

Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "gettransaction",
  "params": {
   "hash":"128170e2de0f96b7fe6f43f2fd64090ab0d63cc43a0f69a04b6e598cd2c70e15"
  }
}
```
Output:
```
{
   "id":"test",
   "jsonrpc":"2.0",
   "result":{
      "status":"OK",
      "transaction":{
         "blockHash":"000000000028e8b92df7010000f0eab92df7010000bd07f628fa7f000050e8b9",
         "blockIndex":0,
         "extra":{
            "nonce":[

            ],
            "publicKey":"8bf1aecc80bf132fded9e1b4464042c04f4df223274e6d501cdbd419d55df9ae",
            "raw":"018bf1aecc80bf132fded9e1b4464042c04f4df223274e6d501cdbd419d55df9ae",
            "size":33
         },
         "fee":100000000000,
         "hash":"491857c7eb6276e0d872c1926d0c9863b39f207ae09d67b70b8bd648e16e82ab",
         "inBlockchain":false,
         "inputs":[
            {
               "data":{
                  "input":{
                     "amount":200000000,
                     "k_image":"982f9b4063268ed8bc2e637db4e5e1195896b696a577f2278b5c2391b98efaee",
                     "key_offsets":[
                        25980,
                        10137,
                        48877
                     ]
                  },
                  "mixin":3,
                  "outputs":[
                     {
                        "number":5,
                        "transactionHash":"227fc58f1c1bdf89698c93a6280ce803cfe76606d6cfce7ef1eed5baf443b45c"
                     },
                     {
                        "number":1,
                        "transactionHash":"dbba432ed02c04540687ea05481ac782686e200efcc489241d08148d1c3fbd0b"
                     },
                     {
                        "number":5,
                        "transactionHash":"76d1c6a06c3049df25430ad2a50d42ec8947ac10b575487ba37f13ef26c17a12"
                     }
                  ]
               },
               "type":"02"
            },

            ...

            {
               "data":{
                  "input":{
                     "amount":3000000000000,
                     "k_image":"17275942b763fc3166ca9b86e6dfcab32ed5a556cc5b995a9c2bbf8a66d7e8d7",
                     "key_offsets":[
                        60338,
                        22276,
                        125912
                     ]
                  },
                  "mixin":3,
                  "outputs":[
                     {
                        "number":10,
                        "transactionHash":"b5c1b064dd0f8ee3ad60e5bb063276d8b49ea50c08487f290e5d525c9c77a4fb"
                     },
                     {
                        "number":92,
                        "transactionHash":"79993ad7abb2a03396129527571f2cd2cab468261e905992f6109d4dfbaebca7"
                     },
                     {
                        "number":4,
                        "transactionHash":"7ffdaefdc2f8d172633d4d22bfab044dcc2bfc44e9c60a4cd250e26af992bb0e"
                     }
                  ]
               },
               "type":"02"
            }
         ],
         "mixin":3,
         "outputs":[
            {
               "globalIndex":0,
               "output":{
                  "amount":9,
                  "target":{
                     "data":{
                        "key":"0d0de439543ff886bbf5d16e1cf4beb9e2163b1a50fadeb461aacf401ccf6351"
                     },
                     "type":"02"
                  }
               }
            },
            
            ...

            {
               "globalIndex":0,
               "output":{
                  "amount":1000000000000,
                  "target":{
                     "data":{
                        "key":"df52982166519417263da2757d91d940bced321807d2e1e97df076cbfd790abf"
                     },
                     "type":"02"
                  }
               }
            }
         ],
         "paymentId":"0000000000000000000000000000000000000000000000000000000000000000",
         "signatures":[
            {
               "first":0,
               "second":"fc770928b3d5ac3a41b68c18e73b64a78e1a46259d1f4139a6a32b408f53720db01a9e4df8443f999bee42263ce5e88f31ab5fababbd69d0db9576775baf970e"
            },
            {
               "first":0,
               "second":"54006f8cbf961549c5cd8e4bb25293493efa6b20d843bd40afc921a0fcd1e40af2a58109b73f8dab78641894bd7a94266ed48b4a8d6355b2c766882617b97d0a"
            },

            ...

            {
               "first":24,
               "second":"3e4d53ae5b46592435d237981e6ad4cb5307e5e9e0d7be546e31bd99d6780a02c18c2847ecb5e8fb3920ae2264c113942b19a3b630157b8dedd8032117c9680c"
            }
         ],
         "signaturesSize":25,
         "size":6577,
         "timestamp":1589473389,
         "totalInputsAmount":5609851418219,
         "totalOutputsAmount":5509851418219,
         "unlockTime":0,
         "version":1
      }
   }
}
```




### gettransactionspool

Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "gettransactionspool",
  "params": {
  }
}
```
Output:
```
{
   "id":"test",
   "jsonrpc":"2.0",
   "result":{
      "status":"OK",
      "transactions":[

      ]
   }
}
```
or 
```
{
   "id":"test",
   "jsonrpc":"2.0",
   "result":{
      "status":"OK",
      "transactions":[
         {
            "amount_out":5880000115000,
            "fee":100000000000,
            "hash":"72b2cdc9d4d3a9def30c7002700a4983120ffb197003f44fce3f43bd2d36d96d",
            "receive_time":1589484795,
            "size":2240
         },
         
         ...

         {
            "amount_out":6512511619736,
            "fee":100000000000,
            "hash":"c3d0f89dec284d2a6479c52544609949f42606315adcfacbb69b79dd6d0fae17",
            "receive_time":1589484796,
            "size":10145
         }
      ]
   }
}
```
