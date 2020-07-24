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


### getblockslist

`getblockslist()` method returns a list of blocks short info.

Argument        | Mandatory     | Description           | Format
--------------- | ------------- | --------------------- | ------
height          | Yes           | The staring height of blocks to be retrieved. | int
count           | No            | The number of blocks to retrieve. | int

**Output**

Argument         | Description          | Format
---------------- | -------------------- | ------
blocks           | The list of block short info | array

block short response attributes:

Argument         | Description          | Format
---------------- | -------------------- | ------
timestamp        | The timestamp of the block | int
height           | The height of the block | int
hash             | The hash of the block | string
transactions_count | The number of transactions in block | int
cumulative_size  | Total size of the block | int
difficulty       | Block's difficulty | int
min_fee          | Minimal transaction fee at the height of the block | int


### getaltblockslist

`getaltblockslist()` method returns a list of alt. blocks short info.

No Input.

**Output**

Argument         | Description          | Format
---------------- | -------------------- | ------
alt_blocks       | The list of block short info | array

Alt. block short response attributes: see [getblockslist](#getblockslist).


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


### getblocktimestamp

`getblocktimestamp()` method returns the timestamp of a block.

**Input**

Argument        | Mandatory     | Description           | Format
--------------- | ------------- | --------------------- | ------
height          | Yes           | height of the block   | int

Argument | Description | Format
------- | ---------- | --------
timestamp | timestamp of the block | int
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


### gettransactionsbypaymentid

`gettransactionsbypaymentid()` methid returns an array of short data of trandactions containing given Payment ID.

**Input**

Argument        | Mandatory     | Description             | Format
--------------- | ------------- | ----------------------- | ------
payment_id      | Yes           | Payment ID              | string

**Output**

Argument | Description | Format
------- | ---------- | --------
status | status of the request | string
transactions | short details of the transactions, see below | array

Short details of the transaction:

Argument | Description | Format
------- | ---------- | --------
hash | the hash of transaction | string
fee | the network fee of transaction | int
amount_out | total amount in transaction | int
size | the size of transaction | int


### gettransactionhashesbypaymentid

`gettransactionhashesbypaymentid()` method returns hashes of transactions containing given Payment ID.

**Input**

Argument        | Mandatory     | Description             | Format
--------------- | ------------- | ----------------------- | ------
paymentId       | Yes           | Payment ID              | string

**Output**

Argument | Description | Format
------- | ---------- | --------
status | status of the request | string
transactionHashes | hashes of transactions | array


### gettransactionsbyhashes

`gettransactionsbyhashes()` method returns details of the transactions found by given hashes.

**Input**

Argument          | Mandatory     | Description             | Format
----------------- | ------------- | ----------------------- | ------
transactionHashes | Yes           | hashes of the transactions to find | array

**Output**

Argument | Description | Format
------- | ---------- | --------
status | status of the request | string
transactions | details of the transactions | array

For transaction details attributes: see [gettransaction](#gettransaction)


### getcurrencyid

`getcurrencyid()` method returns unique currency identifier.

No Input

**Output**

Argument | Description | Format
-------- | ----------- | ------
currency_id_blob | unique currency identifier | string


### checktransactionkey

`checktransactionkey()` method allows to check payment by `Private Transaction Key`.

**Input**

Argument          | Mandatory  | Description             | Format
----------------- | ---------- | ----------------------- | ------
transaction_id    | yes        | the hash of transaction | string
transaction_key   | yes        | Private Transaction Key | string 
address           | yes        | the destination public address | string

**Output**

Argument | Description | Format
-------- | ----------- | ------
amount   | the amount received by destination address | int
outputs  | outputs that belong to destination address | array
status | status of the request | string


### checktransactionproof

`checktransactionproof()` allows to check payment by special Transaction Proof without revealing `Private Transaction Key` by sender.

**Input**

Argument            | Mandatory  | Description             | Format
------------------- | ---------- | ----------------------- | ------
transaction_id      | yes        | the hash of transaction | string
signature           | yes        | The proof of the transaction | string 
destination_address | yes        | the destination public address | string

**Output**

Argument | Description | Format
-------- | ----------- | ------
signature_valid | whether signature is valid | boolean
received_amount | the amount received by destination address | int
outputs  | outputs that belong to destination address | array
status | status of the request | string


### checktransactionbyviewkey

`checktransactionbyviewkey()` method allows to check payment by recipient's `View Secret Key`.

**Input**

Argument          | Mandatory   | Description             | Format
----------------- | ----------- | ----------------------- | ------
transaction_id    | yes         | the hash of transaction | string
view_key          | yes         | recipient's `View Secret Key` | string
address           | yes         | recipient's public address | string

**Output**

Argument | Description | Format
-------- | ----------- | ------
amount | the amount received by destination address | int
outputs  | outputs that belong to destination address | array
confirmations | the number of network confirmations | int
status | status of the request | string


### checkreserveproof

`checkreserveproof()` method allows to check the proof of reserve which proves that given address possess/possessed the said amount at given height. 

**Input**

Argument     | Mandatory   | Description             | Format
------------ | ----------- | ----------------------- | ------
address      | yes         | public address of wallet which reserve | string
height       | no          | the height as of which to check the reserve | int
message      | no          | the challenge message | string
signature    | yes         | the signature proving the balance | string

**Output**

Argument | Description | Format
-------- | ----------- | ------
good     | whether signature is valid | boolean
total    | total amount proved | int
spent    | spent amount | int
locked   | locked amount | int


### validateaddress

`validateaddress()` methods allows to check if given public address is valid.

**Input**

Argument     | Mandatory   | Description             | Format
------------ | ----------- | ----------------------- | ------
address      | yes         | public address to validate | string

**Output**

Argument | Description | Format
-------- | ----------- | ------
is_valid | whether given address is valid | boolean
address  | address, encoded from decoded public keys | string
spend_public_key | decoded spend public key of the address | string
view_public_key | decoded view public key of the address | string
status | status of the request | string


### verifymessage

`verifymessage()` method allows to verify message signed by wallet keys.

**Input**

Argument     | Mandatory   | Description             | Format
------------ | ----------- | ----------------------- | ------
message      | yes         | message to verify       | string
address      | yes         | public address corresponding to keys, used to sign message | string
signature    | yes         | signature of message by private keys | string

**Output**

Argument | Description | Format
-------- | ----------- | ------
sig_valid | whether signature is valid | boolean
status | status of the request | string


### resolveopenalias

`resolveopenalias()` method allows to get address from alias DNS record. Node perfomrs DNS query and returns address if found.

**Input**

Argument     | Mandatory   | Description             | Format
------------ | ----------- | ----------------------- | ------
url          | yes         | OpenAlias domain name   | string

**Output**

Argument | Description | Format
-------- | ----------- | ------
address  | found address correspoding to alias | string
status | status of the request | string


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


### getblockslist

Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "getblockslist",
  "params": {
    "height": 100000,
    "count": 10
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
            "cumulative_size":405,
            "difficulty":18484080,
            "hash":"f9940a120ca47d23e014078d7bbfd59f6ce4f20831a4e011b02ff73fcf0372da",
            "height":100000,
            "min_fee":100000000000,
            "timestamp":1492672031,
            "transactions_count":1
         },

         ...

         {
            "cumulative_size":405,
            "difficulty":24697711,
            "hash":"8f345a2656da4fd1da0c09193ea177af3ac69ea20f1d5090fbc507cc196ed2d6",
            "height":99990,
            "min_fee":100000000000,
            "timestamp":1492668959,
            "transactions_count":1
         }
      ],
      "status":"OK"
   }
}
```


### getaltblockslist

Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "getaltblockslist",
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
      "alt_blocks":[
         {
            "cumulative_size":405,
            "difficulty":13913696485,
            "hash":"2d7cc8c350e1152a9a9178638c09e8c02362c9a19cfe51a3a3722b8a95588afd",
            "height":490523,
            "min_fee":100000000000,
            "timestamp":1590163198,
            "transactions_count":1
         }
      ],
      "status":"OK"
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


### getblocktimestamp

Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "getblocktimestamp",
  "params": {
    "height":10000
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
      "timestamp":1467193202
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


### gettransactionsbypaymentid

Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "gettransactionsbypaymentid",
  "params": {
    "payment_id":"c536d820595b51fdc742ce173c0e6373d1ba3a4eca85f0bac5790030c5d76c91"
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
         {
            "amount_out":6200000070000,
            "fee":100000000000,
            "hash":"6c8cd9e36eb8fe893532eff91347c74443938525c2ca72d8341e6883dd281d71",
            "size":984
         },
         
         ...
         
         {
            "amount_out":20692005138090,
            "fee":100000000000,
            "hash":"d511349c81fb99c97273db687387801b63647f03b9a2acf1a000a1235256818a",
            "size":4463
         }
      ]
   }
}
```


### gettransactionhashesbypaymentid
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "gettransactionhashesbypaymentid",
  "params": {
    "paymentId":"c536d820595b51fdc742ce173c0e6373d1ba3a4eca85f0bac5790030c5d76c91"
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
      "transactionHashes":[
         "6c8cd9e36eb8fe893532eff91347c74443938525c2ca72d8341e6883dd281d71",
         "a71285fcd8afc0d1de2271237294e795f2342b0080f6e79da6b58019427cdeb4",
         "30fb0ce3b4a5a52083f862d3741a5b4a7e595eaaf21e4d0e5e6ca4cc826f0e5f",
         
         ...

         "528126ab6e1a9203d776684b422b98e78c9a865af555efddb0ea9eb29a22d05b"
      ]
   }
}
```


### gettransactionsbyhashes
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "gettransactionsbyhashes",
  "params": {
    "transactionHashes":[
      "6c8cd9e36eb8fe893532eff91347c74443938525c2ca72d8341e6883dd281d71",
      "a71285fcd8afc0d1de2271237294e795f2342b0080f6e79da6b58019427cdeb4"
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
      "status":"OK",
      "transactions":[
         {
            "blockHash":"63f96f2865e5df5d5894ca832446dee652bc791ab9773fdbee200eed38cdd6cc",
            "blockIndex":469284,
            "extra":{
               "nonce":[
                  0,
                  197,
                  
                  ...

                  108,
                  145
               ],
               "publicKey":"cc9b75594145a37be8c43da995cfd32699ad0768b0e5923fc785e0f952f356f5",
               "raw":"022100c536d820595b51fdc742ce173c0e6373d1ba3a4eca85f0bac5790030c5d76c9101cc9b75594145a37be8c43da995cfd32699ad0768b0e5923fc785e0f952f356f5",
               "size":68
            },
            "fee":100000000000,
            "hash":"6c8cd9e36eb8fe893532eff91347c74443938525c2ca72d8341e6883dd281d71",
            "inBlockchain":true,
            "inputs":[
               {
                  "data":{
                     "input":{
                        "amount":300000000000,
                        "k_image":"670705859ea6ada74b698a46e635493783eb4c0cf61f04a10d7a3921147f74ec",
                        "key_offsets":[
                           73283,
                           136011,
                           62294
                        ]
                     },
                     "mixin":3,
                     "outputs":[
                        {
                           "number":10,
                           "transactionHash":"0189418174da81938e69da225538eacb859f2ab7d2af4eb5538ed19a3d031e0e"
                        },
                        {
                           "number":37,
                           "transactionHash":"96ecd2389c47e0b808b24774e63710144a1d1b1853a1d09433c9404e0609d2e2"
                        },
                        {
                           "number":10,
                           "transactionHash":"88a9c50ea7c01914577bb1e9e5f970e1abe4fcb9fcc32923e31fb10f62524624"
                        }
                     ]
                  },
                  "type":"02"
               },
               {
                  "data":{
                     "input":{
                        "amount":70000,
                        "k_image":"0fde58f15f85702514dc73c11f76f4804995e48ff7a3e4132e3a9c26de71f894",
                        "key_offsets":[
                           25177,
                           4837,
                           16455
                        ]
                     },
                     "mixin":3,
                     "outputs":[
                        {
                           "number":3,
                           "transactionHash":"7b6812f52141b949921611b1751d3fa970dd48a32c3f6df25d77838158e7fd6e"
                        },
                        {
                           "number":2,
                           "transactionHash":"62ad89ba56f7236346f072645482f9d3ac12c25162dd96a5c34dd71dd3fa046c"
                        },
                        {
                           "number":3,
                           "transactionHash":"e1d8bf45eab97166cfcdae45615e967cb2d7ef04a13921225edb135ebbde9332"
                        }
                     ]
                  },
                  "type":"02"
               },
               {
                  "data":{
                     "input":{
                        "amount":6000000000000,
                        "k_image":"c1bc732c470e87909449359dc6f1beb431c5bf4e87b6294f6b465a86a57323d6",
                        "key_offsets":[
                           100847,
                           2958,
                           21896
                        ]
                     },
                     "mixin":3,
                     "outputs":[
                        {
                           "number":13,
                           "transactionHash":"4087f0fbaf3d6f388cfffb89024e846eb7bcd16a66a3fbb6c7dac9057f303219"
                        },
                        {
                           "number":11,
                           "transactionHash":"e4aa36188ef77f5b46a1f5caa6de20dd5b588b3e3f2cb777027aa3e7233f05e5"
                        },
                        {
                           "number":12,
                           "transactionHash":"4a43d417edbd78079bd133c5108e45557b915cff41a4d08e9b03fc1427278153"
                        }
                     ]
                  },
                  "type":"02"
               }
            ],
            "mixin":3,
            "outputs":[
               {
                  "globalIndex":46652,
                  "output":{
                     "amount":70000,
                     "target":{
                        "data":{
                           "key":"af027f1a2951309a41a81b5a8bafe1f18b573f63b67b700f8b90d24fa12c3432"
                        },
                        "type":"02"
                     }
                  }
               },
               
               ...

               {
                  "globalIndex":201436,
                  "output":{
                     "amount":3000000000000,
                     "target":{
                        "data":{
                           "key":"6f7faf1dbf245c561c79eb6e1b5aabd4304e06d879c28c8fafb0ffa08a602e8f"
                        },
                        "type":"02"
                     }
                  }
               }
            ],
            "paymentId":"c536d820595b51fdc742ce173c0e6373d1ba3a4eca85f0bac5790030c5d76c91",
            "signatures":[
               {
                  "first":0,
                  "second":"0856318f727192193f1b7471932ad238b21e323a6220a2bcbb156538b09a9e0b5f46e97e1080e7f00574ea32abb3a4e492540f3da90442cbd0e1617ed4f4ed03"
               },
               
               ...

               {
                  "first":2,
                  "second":"760ab2d47102578295e8ad01231ce20f43d206861dc85c66632fc48bcfe86e0196fd8f146c830da43fccf395564b70cc15fba2629c1af981e5cbd75fd4c2d709"
               }
            ],
            "signaturesSize":3,
            "size":984,
            "timestamp":1585028829,
            "totalInputsAmount":6300000070000,
            "totalOutputsAmount":6200000070000,
            "unlockTime":0,
            "version":1
         },
         {
            "blockHash":"99594aa44c83a261bfc408d563e2bc67dfc3e357691c8bb4b24dde072149d7d7",
            "blockIndex":469381,
            "extra":{
               "nonce":[
                  0,
                  197,
                  
                  ...

                  145
               ],
               "publicKey":"9e6286c03a8a96fcdf5e60fac543a8fe89705b24c734ffdbca895aebf9b49368",
               "raw":"022100c536d820595b51fdc742ce173c0e6373d1ba3a4eca85f0bac5790030c5d76c91019e6286c03a8a96fcdf5e60fac543a8fe89705b24c734ffdbca895aebf9b49368",
               "size":68
            },
            "fee":100000000000,
            "hash":"a71285fcd8afc0d1de2271237294e795f2342b0080f6e79da6b58019427cdeb4",
            "inBlockchain":true,
            "inputs":[
               {
                  "data":{
                     "input":{
                        "amount":80000000000,
                        "k_image":"7c505592f87c678a19de6d55695e1f9ca51eebca9f5fc1090ff492961e411c90",
                        "key_offsets":[
                           57363,
                           48962,
                           9654
                        ]
                     },
                     "mixin":3,
                     "outputs":[
                        {
                           "number":3,
                           "transactionHash":"1b34655c1b6598988b1206dfd62dc42fbe61ab3003076a2c2994f90294c99069"
                        },
                        {
                           "number":8,
                           "transactionHash":"5c2b7ab136eb5051785be0fef8d421fb85a6eee24599a94673b992adf5339a86"
                        },
                        {
                           "number":6,
                           "transactionHash":"6a87c5f1c71e24f4a722b45c3c4971efd8f539ed7f243a47ec19beeda1abb6e6"
                        }
                     ]
                  },
                  "type":"02"
               },
               {
                  "data":{
                     "input":{
                        "amount":2000000000,
                        "k_image":"1f887b2d19c7c3896371c484bd7db755ac5d0b15139f30712646e8f93525f83a",
                        "key_offsets":[
                           56150,
                           21092,
                           22361
                        ]
                     },
                     "mixin":3,
                     "outputs":[
                        {
                           "number":2,
                           "transactionHash":"aa4d0bc51b4a174dfbb6784fd9923762e290b578f7ed63ddf5f7f514e185ee3b"
                        },
                        {
                           "number":8,
                           "transactionHash":"2d157946f5ccb7e36e6e35d4873b3271a9c5de4c76787650ee01fcad5415939c"
                        },
                        {
                           "number":8,
                           "transactionHash":"e30747b1c95626b821f7ff9a914fab6af3b11fff34a719e6430095a3b85c64d4"
                        }
                     ]
                  },
                  "type":"02"
               },
               {
                  "data":{
                     "input":{
                        "amount":50000,
                        "k_image":"c736d6cd104baabb88781da7360cde367ec64fb366c1fe71e0057bcd9babeb10",
                        "key_offsets":[
                           31474,
                           3302,
                           13087
                        ]
                     },
                     "mixin":3,
                     "outputs":[
                        {
                           "number":1,
                           "transactionHash":"eca2a57c52ce4f3a7b7e795b20eef10211306da199f65a89cf100b622e9fdfc5"
                        },
                        {
                           "number":4,
                           "transactionHash":"d367618fcec07a38c9790d850bf1b78b3a706bda3cb0eeac067ac2555748f059"
                        },
                        {
                           "number":4,
                           "transactionHash":"f750d925fef28077ade3cbcfd829256ffbb45f806d7c3d6fdf0e9fb1f6155cf0"
                        }
                     ]
                  },
                  "type":"02"
               },
               {
                  "data":{
                     "input":{
                        "amount":1000000000000,
                        "k_image":"4a802ba8a9a1776a5d4c966af3468c9858de835bcfd76baedc94752eb33e5c09",
                        "key_offsets":[
                           450585,
                           265093,
                           305164
                        ]
                     },
                     "mixin":3,
                     "outputs":[
                        {
                           "number":28,
                           "transactionHash":"8b069352c1b011bdbfa3d15cbbe8c555693a0b981f42d67f12c7781e78fad903"
                        },
                        {
                           "number":52,
                           "transactionHash":"b77a1f4b74377c9b353c3a7b0db972a5f5447a01f8ac147155cd128b0493cd6c"
                        },
                        {
                           "number":10,
                           "transactionHash":"94c4f1517d3a416b13a82a1a598864616e137ae887de5d7422462753a7680eef"
                        }
                     ]
                  },
                  "type":"02"
               },
               {
                  "data":{
                     "input":{
                        "amount":6000000000000,
                        "k_image":"4c9f3fd03425c5027b599c024e5d35cb46ce4dd3ee4aad47f4417ebbeada1247",
                        "key_offsets":[
                           71875,
                           20901,
                           32218
                        ]
                     },
                     "mixin":3,
                     "outputs":[
                        {
                           "number":5,
                           "transactionHash":"a2b15b4e6507df28222b44d316f46dcbf9fe8f5ca57ab73ee77646d1581e7e9a"
                        },
                        {
                           "number":6,
                           "transactionHash":"bf1d927763d34bd30e5e0d58eaa46292bce63832a12b55d02e1269f7db650c9d"
                        },
                        {
                           "number":10,
                           "transactionHash":"d81f46209a8d8db45fedb93b5bd51af3fdadbfc26cc1cb10c6a0c96bc2fadbae"
                        }
                     ]
                  },
                  "type":"02"
               }
            ],
            "mixin":3,
            "outputs":[
               {
                  "globalIndex":48133,
                  "output":{
                     "amount":50000,
                     "target":{
                        "data":{
                           "key":"25bc53225e619945f947af8b912c822e617e21714c248b11658eba32e0cd5954"
                        },
                        "type":"02"
                     }
                  }
               },
               
               ...

               {
                  "globalIndex":201465,
                  "output":{
                     "amount":3000000000000,
                     "target":{
                        "data":{
                           "key":"4caeb6b3b5becae0d28eed651f02d70af72c811e0035494753ca8d35c9ef8bed"
                        },
                        "type":"02"
                     }
                  }
               }
            ],
            "paymentId":"c536d820595b51fdc742ce173c0e6373d1ba3a4eca85f0bac5790030c5d76c91",
            "signatures":[
               {
                  "first":0,
                  "second":"e213c7baa1c04f4ee504e28f8abcb6c076b9140d56364c727cd043400268a60d0e4fc2a015b435eb4a7c6510bc602240b4f8a4004921872e98e985179865df06"
               },
               
               ...

               {
                  "first":4,
                  "second":"d6819e1538523552006d30a8aa05c48cbd93fb491ad8a09cc7efdb5a3a81360a440dc56c3b6cafc9e03288fe1e21178dd4a1cdf11b9b9062f6594ac1ad5c9e01"
               }
            ],
            "signaturesSize":5,
            "size":1541,
            "timestamp":1585053091,
            "totalInputsAmount":7082000050000,
            "totalOutputsAmount":6982000050000,
            "unlockTime":0,
            "version":1
         }
      ]
   }
}
```


### checktransactionkey
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "checktransactionkey",
  "params": {
    "transaction_id": "494862266B7E511A4F901E7A0EFFB27B012ABA4447D4B0666A010781B7A6FBE5",
    "address": "KhnaNiHdEdWcLh8VseUa8Z2fv2e6w2rvWgYySWZaEUMSCHFqhJyhWXY6tUeYsqSZ31QANbaZP6Gm7byZomD4xsc9QMye6ZX",
    "transaction_key": "43210C433EAE73271779652F67DFF20B03591776FE76FEA4FD55D69F237CBC0D"
  }
}
```
Output:
```
{
   "id":"test",
   "jsonrpc":"2.0",
   "result":{
      "amount":300000000000000,
      "outputs":[
         {
            "amount":300000000000000,
            "target":{
               "data":{
                  "key":"a5bfae862500ab22e600ff90fb7052960fa2e0abb4d129c6c4b494cc4be1337f"
               },
               "type":"02"
            }
         }
      ],
      "status":"OK"
   }
}
```


### checktransactionproof
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "checktransactionproof",
  "params": {
    "transaction_id": "2196e40ff4bcd7711f57d7ccd2aab67f8dddf6015ad72ae2b4d63621521a94a9",
    "destination_address": "Kiwr4Aajn7QefxbAEvHSAcTrVbhzYukfmbDvwWkrDhjFXe1FVUa5ggxCrEv4w2zvaiVZgoF4v7b3cNAbaU3LKQGS9EU9KAd",
    "signature": "ProofR3Y7go5QVgEx8zvs4LWQ5ghzRifmUtLDXYhEMm2Ku9idhg8S3NEM4eeWDZbGEFCdn6H4GoyZcnQ2FHWb8hteHD3BkGBYDbZ1hA7xoRGY9DX9xCSXSQ2Xb7HDXARjX4YjGfyAWgGZ9f"
  }
}
```
Output:
```
{
   "id":"test",
   "jsonrpc":"2.0",
   "result":{
      "confirmations":23294,
      "outputs":[
         {
            "amount":100000000000,
            "target":{
               "data":{
                  "key":"de5a651865919d253d08b88bf78f3923f02f9f4002219f23f2bfdc6fac5a9ff6"
               },
               "type":"02"
            }
         },
         {
            "amount":2000000000000,
            "target":{
               "data":{
                  "key":"5f4feea8da71e322dd60c1057ffe80d288322f211ab30e817889d71bc134d040"
               },
               "type":"02"
            }
         }
      ],
      "received_amount":2100000000000,
      "signature_valid":true,
      "status":"OK"
   }
}
```


### checktransactionbyviewkey
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "checktransactionbyviewkey",
  "params": {
    "transaction_id": "462266B7E511A4F901E7A0EFFB27B012ABA4948447D4B0666A010781B7A6FBE5",
    "address": "Kiwr4Aajn7QefxbAEvHSAcTrVbhzYukfmbDvwWkrDhjFXe1FVUa5ggxCrEv4w2zvaiVZgoF4v7b3cNAbaU3LKQGS9EU9KAd",
    "view_key": "4bcd75aef0eaf0c1e34caf024cc1f499a7656083e4921e58552c3c1254e99209"
  }
}
```
Output:
```
{
   "id":"test",
   "jsonrpc":"2.0",
   "result":{
      "amount":599900000600000,
      "confirmations":5018,
      "outputs":[
         {
            "amount":600000,
            "target":{
               "data":{
                  "key":"09f79dc4a9c0cc6e32be6cb32a70cc4a4f9f09185627d234470d830004e665eb"
               },
               "type":"02"
            }
         },

         ...

         {
            "amount":500000000000000,
            "target":{
               "data":{
                  "key":"21d49839518f2d07524e6710093cdbcedfe4076265f851d117925d18e01ee628"
               },
               "type":"02"
            }
         }
      ],
      "status":"OK"
   }
}
```


### checkreserveproof
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "checkreserveproof",
  "params": {
    "address": "Kiwr4Aajn7QefxbAEvHSAcTrVbhzYukfmbDvwWkrDhjFXe1FVUa5ggxCrEv4w2zvaiVZgoF4v7b3cNAbaU3LKQGS9EU9KAd",
    "height":489000,
    "message": "this is challenge message",
    "signature": "RsrvPrf......"
  }
}
```
Output:
```
{
   "id":"test",
   "jsonrpc":"2.0",
   "result":{
      "good":true,
      "locked":0,
      "spent":0,
      "total":103143982017908
   }
}
```


### validateaddress
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "validateaddress",
  "params": {
    "address": "Kd79ZmERRBx3t5uuERi6ggTMMeTBDTLY21cvkEFtE29GY8FJuwQHmWyRxYbPxYBu8S8a7wzxhg3tJfbE27hYGYtbD4mGiSs"
  }
}
```
Output:
```
{
   "id":"test",
   "jsonrpc":"2.0",
   "result":{
      "address":"Kd79ZmERRBx3t5uuERi6ggTMMeTBDTLY21cvkEFtE29GY8FJuwQHmWyRxYbPxYBu8S8a7wzxhg3tJfbE27hYGYtbD4mGiSs",
      "is_valid":true,
      "spend_public_key":"56359b8d0f44eb113916a3dfdcceb99d8ac8b904d7e8c303b40b6e8356c3bbba",
      "status":"OK",
      "view_public_key":"1578f4ff1adf2a95364f118ef2f05f2d43a50693d3491fe6b709ff7db9ea546a"
   }
}
```


### verifymessage
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "verifymessage",
  "params": {
    "message": "test",
    "address": "Kiwr4Aajn7QefxbAEvHSAcTrVbhzYukfmbDvwWkrDhjFXe1FVUa5ggxCrEv4w2zvaiVZgoF4v7b3cNAbaU3LKQGS9EU9KAd",
    "signature": "SigV1RwnRhiLR8MU2S55xj9kEt119U4JcEzbToamAbsZ9qzRD3tDxUEBCCWMNDKCeGqDh25g6Wguq9Fio4SteFfwkUSZP"
  }
}
```
Output:
```
{
   "id":"test",
   "jsonrpc":"2.0",
   "result":{
      "sig_valid":true,
      "status":"OK"
   }
}
```

### resolveopenalias
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "resolveopenalias",
  "params": {
   "url":"aiwe.karbo.me"
  }
}
```
Output:
```
{
  "id": "test",
  "jsonrpc": "2.0",
  "result": {
    "address": "KetKFqZu4jH9Gnbbvp5ckbXBzadeDK6EFPNFuPcZcCjMDK31r84weVzcF2BhewZEQGZUjDTB7QgHVbJoYTE89eh2ETuDdLH",
    "status": "OK"
  }
}
```
