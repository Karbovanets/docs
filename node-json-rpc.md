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

`gettransactionspool()` method returns the list of short details of transactions present in mempool.

No Input

**Output**

Argument | Description | Format
------- | ---------- | --------
status | status of the request | string
transactions | array of transactions in mempool* | array

\* Empty array means that currently there are no transactions in mempool.

Transactions entry attributes:

Argument | Description | Format
------- | ---------- | --------
hash | the hash of transaction | string
fee | the network fee of transaction | int
amount_out | total amount in transaction | int
size | the size of transaction | int
receive_time | the timestamp when transaction was received by queried node | int


### gettransactionsinpool

`gettransactionsinpool()` method returns the list of transactions details that are in mempool. 

No Input

**Output**

Argument | Description | Format
------- | ---------- | --------
status | status of the request | string
transactions | array of transactions in mempool* | array

\* Empty array means that currently there are no transactions in mempool.

See [gettransaction](#gettransaction) for attributes of `transactions`.


### getrawtransactionspool

`getrawtransactionspool()` method returns the list of transactions in mempool consisting of raw transactions with additional details and output indexes. 

No Input

Argument | Description | Format
------- | ---------- | --------
status | status of the request | string
transactions | array of transactions in mempool* | array

\* Empty array means that currently there are no transactions in mempool.

See [getrawtransactionsbyheights](#getrawtransactionsbyheights) for attributes of `transactions`.


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

For `transactions` details attributes: see [gettransaction](#gettransaction)


### gettransactionsbyheights

`gettransactionsbyheights()` method returns details of the transactions from blocks by requested heights.

**Input**

Argument           | Mandatory     | Description             | Format
------------------ | ------------- | ----------------------- | ------
heights            | yes           | heights of blocks from which to serve transactions | array
include_miner_txs  | no            | whether include coinbase transactions | bool
exclude_signatures | no            | whether to exclude signatures of transactions | bool
range              | no            | whether `heights` argument contains a list of blocks or a range (first and last height); if set to `true` transactions from all blocks in a rage are served | bool

**Output**

Argument     | Description | Format
------------ | ---------- | --------
status       | status of the request | string
missed_txs   | list of hashes of missed transactions if any (unlikely to happen) | array
transactions | details of the transactions | array

For `transactions` details attributes: see [gettransaction](#gettransaction)


### getrawtransactionsbyheights

`getrawtransactionsbyheights()` method returns raw transactions with output global indexes from in blocks by requested heights.

**Input**

Argument           | Mandatory     | Description             | Format
------------------ | ------------- | ----------------------- | ------
heights            | yes           | heights of blocks from which to serve transactions | array
include_miner_txs  | no            | whether include coinbase transactions | bool
range              | no            | whether `heights` argument contains a list of blocks or a range (first and last height); if set to `true` transactions from all blocks in a rage are served | bool

**Output**

Argument     | Description | Format
------------ | ---------- | --------
status       | status of the request | string
missed_txs   | list of hashes of missed transactions if any (unlikely to happen) | array
transactions | list of raw transaction prefixes and corresponding output global indexes | array

Each entry in `transactions` consists of:

Argument       | Description | Format
-------------- | ---------- | --------
block_hash     | the hash of block containing transaction \* | string
fee            | the network fee of transaction | int
hash           | the hash of transaction | string
height         | the height of block containing transaction \*\* | int
output_indexes | the list of output global indexes | array
timestamp      | the timestamp of block containing transaction \*\*\* | int
transaction    | transaction prefix (transaction without signatures) | json object

\* null hash if transaction is not in a block (is in mempool)

\*\* invalid height if transaction is not in a block (is in mempool)

\*\*\* node's receive time if transaction is not in a block (is in mempool)

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
status   | status of the request | string


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


### checkpayment

`checkpayment()` allows checking payment to given `address` by given `payment id`. It basically combines the functionality of several separate methods in a single convenience method. This method allows to do the payment in several transactions until the total received amount satisfies the requested one, i.e. it allows payment from several wallets, group payment etc.

**Request**
Argument        | Mandatory     | Description           | Format
--------------- | ------------- | --------------------- | ------
address         | yes | Receiving public address | string
amount          | yes | Amount to be paid | int      
payment_id      | yes | Unique Payment Id of the operation | string
view_key        | yes | The *Private View Key* of the receiving address | string

**Response**

Argument         | Description          | Format
---------------- | -------------------- | ------
confirmations    | The number of network confirmations of the paying transaction(s) (largest in case of several transactions) | int
received_amount  | The amount received in AU | int
status | Status of payment | string
transaction_hashes | Hashes of transactions with given Payment ID actually paying to provided address | array 

`status` can be:
- `paid`, 
- `underpaid`, 
- `pending`, 
- `not_found`


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


### gettransactionsinpool

Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "gettransactionsinpool",
  "params": {
  }
}
```
Output:
```
{
    "id": "test",
    "jsonrpc": "2.0",
    "result": {
        "status": "OK",
        "transactions": [
            {
                "blockHash": "0000000000000000000000000000000000000000000000000000000000000000",
                "blockIndex": 0,
                "extra": {
                    "nonce": [],
                    "publicKey": "983f8a711735dfbffdaf929c4e6f90eeaabb3d916d1b5439020037d82c105c98",
                    "raw": "01983f8a711735dfbffdaf929c4e6f90eeaabb3d916d1b5439020037d82c105c98",
                    "size": 33
                },
                "fee": 100000000000,
                "hash": "be74a4f11c735331d49a64383005e7d8dfc5198eb44d2c484ffa09b05f291c13",
                "inBlockchain": false,
                "inputs": [
                    {
                        "data": {
                            "input": {
                                "amount": 10000,
                                "k_image": "64cfbc84badc80b713462d88d7510d4cebbd62468b8b99db49fa4508ba9978b4",
                                "key_offsets": [
                                    29402,
                                    28079,
                                    14489
                                ]
                            },
                            "mixin": 3,
                            "outputs": [
                                {
                                    "number": 4,
                                    "transactionHash": "c564e13e0e50c71dfafff9fcb5b51dc4b00f6c146635844d88594b9a01344417"
                                },
                                {
                                    "number": 2,
                                    "transactionHash": "d997f7824a4ce593caef7134a28192ed23cb90f483187f71b2308574424af748"
                                },
                                {
                                    "number": 3,
                                    "transactionHash": "ff8ec5acca5158e3c228f9b37479a243f2e8845d9fa3c4e454a9bdb7dcf099be"
                                }
                            ]
                        },
                        "type": "02"
                    },
                    ...
                ],
                "mixin": 3,
                "outputs": [
                    {
                        "globalIndex": 0,
                        "output": {
                            "amount": 10000,
                            "target": {
                                "data": {
                                    "key": "579b952e364f7c7b2007632173175ba4dcec0b15c2c26b8fbe2f361dc0fe5f60"
                                },
                                "type": "02"
                            }
                        }
                    },
                    ...
                ],
                "paymentId": "0000000000000000000000000000000000000000000000000000000000000000",
                "signatures": [
                    {
                        "first": 0,
                        "second": "daa3599557a78114df9197c30eb1561bde1233876a13567e89a43b8cfd85f405a70f6f294f27d9c47d481b525ed8ff2fce2da2bc7ebdd18a39ceb18c841eb606"
                    },
                    ...
                    {
                        "first": 2,
                        "second": "fd728efd21f7eca453c05c7b618b05e57dddb4f2cd63ed2b08c0f0b69b16020a4b10016910e4fd616be3b4cd14be307a135b6e9fa13bab9ba777cc96a7108806"
                    }
                ],
                "signaturesSize": 3,
                "size": 981,
                "timestamp": 1607253285,
                "totalInputsAmount": 4000040010000,
                "totalOutputsAmount": 3900040010000,
                "unlockTime": 0,
                "version": 1
            },
            ...
        ]
    }
}
```


### getrawtransactionspool

Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "getrawtransactionspool",
  "params": {
   
  }
}
```
Output:
```
{
    "id": "test",
    "jsonrpc": "2.0",
    "result": {
        "status": "OK",
        "transactions": [
            {
                "block_hash": "0000000000000000000000000000000000000000000000000000000000000000",
                "fee": 100000000000,
                "hash": "d22966b99f903e873b2bf8a95490da4b44c84a77218b0ed4092900fe38769168",
                "height": 0,
                "output_indexes": [],
                "timestamp": 1607255955,
                "transaction": {
                    "extra": "01b42900844234fba05c082f9de4a56bfb8bc392bfb99a89fc38414d7dc07ccb5c",
                    "unlock_time": 0,
                    "version": 1,
                    "vin": [
                        {
                            "type": "02",
                            "value": {
                                "amount": 500000000,
                                "k_image": "9a1b9398882b915e26f57ccfe60a8de4999e2c28cf8815f55ee6dd9abf4271f1",
                                "key_offsets": [
                                    42528,
                                    10598,
                                    46592
                                ]
                            }
                        },
                        ...
                        {
                            "type": "02",
                            "value": {
                                "amount": 2000000000000,
                                "k_image": "43586f1249710b4c271587bc85a60a2498dba901495bd3f98d6d212687a823e6",
                                "key_offsets": [
                                    132076,
                                    17225,
                                    234343
                                ]
                            }
                        }
                    ],
                    "vout": [
                        {
                            "amount": 400,
                            "target": {
                                "data": {
                                    "key": "756c488dc5bfd186f0e59c75c45e9d342b67ddb35d0ec017ade9ad89229b3baf"
                                },
                                "type": "02"
                            }
                        },
                        ...
                        {
                            "amount": 2000000000000,
                            "target": {
                                "data": {
                                    "key": "019c15ae6762c0ea0a45f840e8c0e53e5713162c6a11bb341f5111e2dd43474b"
                                },
                                "type": "02"
                            }
                        }
                    ]
                }
            },
            ...
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
               ...
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
         ...
      ]
   }
}
```


### gettransactionsbyheights
Input:
```
{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "gettransactionsbyheights",
    "params": {
        "heights": [
            544404,
            544406
        ],
        "include_miner_txs": false,
        "exclude_signatures": true,
        "range": true
    }
}
```
Output:
```
{
    "id": 0,
    "jsonrpc": "2.0",
    "result": {
        "missed_txs": [],
        "status": "OK",
        "transactions": [
            {
                "blockHash": "b83ebada751cd090496998a0fea7a45cd121d72db1f33746025e2b3a2243069c",
                "blockIndex": 544404,
                "extra": {
                    "nonce": [],
                    "publicKey": "9425a5c99043505b1d314d91a05f958821240c58f5e6b66b6b2cf5fe5ae1bd28",
                    "raw": "019425a5c99043505b1d314d91a05f958821240c58f5e6b66b6b2cf5fe5ae1bd28",
                    "size": 33
                },
                "fee": 100000000000,
                "hash": "f95fd90c6e0da58bf6ee415b1267bb6e37ce972a286362ae3dced475f0c8ccac",
                "inBlockchain": true,
                "inputs": [
                    {
                        "data": {
                            "input": {
                                "amount": 2000000000,
                                "k_image": "6dcfcc11b018ce42a775718f5ed98729d840ed3eb2a41dc6acd1334ba1008531",
                                "key_offsets": [
                                    35996,
                                    48718,
                                    6576,
                                    13024,
                                    557,
                                    5926
                                ]
                            },
                            "mixin": 6,
                            "outputs": [
                                {
                                    "number": 2,
                                    "transactionHash": "03d39a62a3e08d6ccbf13c175c9b32aade96e84e4c6aba29a52ab7c273dbdee3"
                                },
                                ...
                                {
                                    "number": 8,
                                    "transactionHash": "887d5aac143f4964d5aa692956537681887e037aa5f2918a5811cfd2a1a3190c"
                                }
                            ]
                        },
                        "type": "02"
                    },
                    ...
                ],
                "mixin": 6,
                "outputs": [
                    {
                        "globalIndex": 113863,
                        "output": {
                            "amount": 2000000000,
                            "target": {
                                "data": {
                                    "key": "7bab078eead6c06f5ea4ce4e203811fea2492cc5150be976baf74a7a2c564fb5"
                                },
                                "type": "02"
                            }
                        }
                    },
                    ...
                ],
                "paymentId": "0000000000000000000000000000000000000000000000000000000000000000",
                "signatures": [],
                "signaturesSize": 0,
                "size": 1187,
                "timestamp": 0,
                "totalInputsAmount": 4002000000000,
                "totalOutputsAmount": 3902000000000,
                "unlockTime": 0,
                "version": 1
            },
            ...
        ]
    }
}
```


### getrawtransactionsbyheights
Input:
```
{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "getrawtransactionsbyheights",
    "params": {
        "heights": [
            544404,
            544406
        ],
        "include_miner_txs": false,
        "range": true
    }
}
```
Output:
```
{
    "id": 0,
    "jsonrpc": "2.0",
    "result": {
        "missed_txs": [],
        "status": "OK",
        "transactions": [
            {
                "block_hash": "3de29c13b41dc89afc3566a040b41a4f5b566eaf73f4f4fc10faa5a482a89736",
                "fee": 100000000000,
                "hash": "03bfe202e4216603f9cf9f501d1b153f15256e23e9d2a8f6fe06904901ab278a",
                "height": 544404,
                "output_indexes": [
                    57191,
                    57629,
                    68772,
                    112691,
                    60331,
                    60723,
                    60626,
                    99123,
                    113862,
                    130215,
                    193459
                ],
                "timestamp": 1603193189,
                "transaction": {
                    "extra": "019425a5c99043505b1d314d91a05f958821240c58f5e6b66b6b2cf5fe5ae1bd28",
                    "unlock_time": 0,
                    "version": 1,
                    "vin": [
                        {
                            "type": "02",
                            "value": {
                                "amount": 2000000000,
                                "k_image": "6dcfcc11b018ce42a775718f5ed98729d840ed3eb2a41dc6acd1334ba1008531",
                                "key_offsets": [
                                    35996,
                                    48718,
                                    6576,
                                    13024,
                                    557,
                                    5926
                                ]
                            }
                        },
                        ...
                    ],
                    "vout": [
                        {
                            "amount": 2000000000,
                            "target": {
                                "data": {
                                    "key": "7bab078eead6c06f5ea4ce4e203811fea2492cc5150be976baf74a7a2c564fb5"
                                },
                                "type": "02"
                            }
                        },
                        ...
                    ]
                }
            },
            ...
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


### checkpayment
Input:
```
{
   "jsonrpc":"2.0",
   "method":"checkpayment",
   "params":{
      "payment_id":"0bdde0dc45636835319012fe55a4823ee30df2fa84444f81e95f891c48987bdf", 
      "view_key":"4ff203c944b6537ff160e328aaa3745a6e50c2bf608161f607b661452eebc5e1",
      "address":"KaqCQAbx3BSKKv7ED98oQP9QSP3igqgo47hPYZ8q6KZyUY6GnDaQkh9WbVR4DxvmCq8mZcKPg3wfWFJQ5CsyrxPqKcXC3rx",
      "amount": 100000000000000
   }
}
```
Output:
```
{
   "jsonrpc": "2.0",
   "result": {
      "confirmations": 80077,
      "received_amount": 1022227324533,
      "status": "paid",
      "transaction_hashes": [
         "01c970533dcfe74f4cacce23997b52f88dda62277a2d720f701ee791f3fcc759"
      ]
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
