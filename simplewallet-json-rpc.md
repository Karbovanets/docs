To start wallet JSON RPC API server you should specify a port on which server binds (additionally to standard wallet's arguments). You can choose any free port. To do that execute the following command from the command line:
```
 simplewallet --wallet-file=example_wallet.bin --pass=12345 --rpc-bind-port=32348
```
Having done that you're ready to operate with the wallet through the following API URLs (e.g., your IP address is 95.46.98.64):

 http://95.46.98.64:32348/json_rpc
 http://localhost:32348/json_rpc


*Note.* It is also possible to run JSON RPC API server in GUI Wallet Classic. To do so, in the menu select "Wallet RPC interface" and check "Run Wallet RPC interface". There you can set URL and port where wallet should listen, as well as set authorisation if needed.

## Available commands ##

* change_password
* get_address
* get_balance
* get_height
* get_paymentid
* get_payments
* get_reserve_proof
* get_transfers
* get_last_transfers
* get_transaction
* get_tx_key
* get_tx_proof
* query_key
* reset
* sign_message
* stop_wallet
* store
* transfer
* validate_address
* verify_message
* estimate_fusion
* send_fusion


Please note, there is no "refresh" RPC method. RPC wallet refresh is performed automatically each 20 seconds.


### change_password

Method used to change the wallet's password.

URL:
```
 /json_rpc
```
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "change_password",
  "params": {
     "old_password":"12345",
     "new_password": "123456"
  }
}
```
Output:
```
{
    "id": "test",
    "jsonrpc": "2.0",
    "result": {
        "password_changed": true
    }
}
```


### get_address

Get public address of this wallet.

URL:
```
 /json_rpc
```
Input: 
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "get_address",
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
        "address": "KfXkT5VmdqmA7bWqSH37p87hSXBdTpTogN4mGHPARUSJaLse6jbXaVbVkLs3DwcmuD88xfu835Zvh6qBPCUXw6CHK8koDCt"
    }
}
```


### get_balance

Return balance.

URL:
```
 /json_rpc
```
Input: 
```
 {
 	"jsonrpc": "2.0", 
 	"method": "get_balance", 
 	"params": {}
 }
```
Output:
```
{
    "jsonrpc": "2.0",
    "result": {
        "available_balance": 0,
        "locked_amount": 0
    }
}
```


### get_height

Returns the last top known block height for simplewallet. This method can be used to verify that simplewallet is correctly synchronized.

URL:
```
 /json_rpc
```
Input:
```
{
 	"jsonrpc":"2.0",
 	"method":"get_height",
 	"params":{
 	}
}
```
Output:
```
{
    "jsonrpc": "2.0",
    "result": {
        "height": 633691
    }
}
```


### get_paymentid

Is used to generate random Payment Id.

URL:
```
 /json_rpc
```
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "get_paymentid",
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
        "payment_id": "800b468ea39d5844de87f9235c3cb74f6a7d5fc61cc61e407d4e6fbfccee412b"
    }
}
```


### get_payments

Receives all the payments with a corresponding *payment_id* that were sent to the wallet. This method is used to get the KRB payments for the 3rd party services. As `simplewallet` uses only one address to receive KRB deposits, a unique *payment_id* should be assigned and shown to each user. The method will return all the payments for this user.

URL:
```
 /json_rpc
```
Input: 
```
{
 	"jsonrpc":"2.0",
 	"method":"get_payments",
 	"params":{
 		"payment_id": "78cc4b76a48bd50ab955ac61a0c04e4a82079fbcf27298f87b39c76aefccbcc9"
 	}
}
```
Output: 
```
 {
    "jsonrpc": "2.0",
    "result": {
        "payments": []
    }
}
```


### get_reserve_proof

Method used to get the proof of balance.

URL:
```
 /json_rpc
```
Input:
```
{
 	"jsonrpc":"2.0",
 	"method":"get_reserve_proof",
 	"params":{
         "amount":100,
         "message": ""
 	}
}
```
Output:
```
{
    "jsonrpc": "2.0",
    "result": {
        "signature": "RsrvPrfuDM9gJtkhU6av4g53nTnFunKz5hQoNSetFhtQ27vDk5LnRrHYTp9ph4ekXg7irP6i94joRAnGYBZdJFNMeBNfUoQkEEkhQPDi2pH8wJ7ECpbxYjbKJJtFmKVG74mFDH78h3edtKWhfb8qKz6hXmVRD7nRC73zFWHKNtbAYVfoVoZZZ3aERnPMEBHEzsqBaUXf7cJHH62cJKiZ23j8yV3N3ey5siXqrWBhv6Vxjb8vm83FbfwR5ZfeDRsHsyieRQCBJggfYWW3r1Zfr1XR8h2v6nAxLPueAmSBFJeYGwufJnpMhLzLXx7juVHXopqEL94bGUN24HufFvagT2zgH7xmVTtuGTn7GkR4a8qQgCu6Be3EXuFHQ4FC4PTtxDbdtxeshXtbAAkBK4TDg3r54vy6h"
    }
}
```


### get_transfers

Returns the list of all the wallet's incoming and outgoing transfers. For the transfers created by simplewallet of previous versions this method returns not exact transfers amounts but the transaction amounts (transfer amount + change).

URL: 
```
 /json_rpc
```
Input:
```
{
 	"jsonrpc":"2.0",
 	"method":"get_transfers",
 	"params":{
 	}
}
```
Output:
```
 {
    "jsonrpc": "2.0",
    "result": {
        "transfers": [
            {
                "address": "",
                "amount": 0,
                "blockIndex": 600103,
                "confirmations": 3588,
                "fee": 0,
                "output": false,
                "paymentId": "",
                "time": 1599044696,
                "transactionHash": "29744bde27281f15065d10f144ed8044695821dbee236356e96eae38615d764b",
                "txKey": "",
                "unlockTime": 140698800195355
            },
            ...
        ]
    }
}
```


### get_last_transfers

Same as `get_transfers` except it returns no all transfers but last *n*. There is a `count` param to specify how many last transactions to fetch.

URL: 
```
 /json_rpc
```
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "get_last_transfers",
  "params": {
   "count":100
  }
}
```

Output is the same as in `get_transfers` method.


### get_transaction

Gets details of particular transaction by it's hash.

Note: if wallet contains no transaction details e.g. because it has been reset, some fields may be empty.

URL:
```
 /json_rpc
```
Input:
```
{
 	"jsonrpc":"2.0",
 	"method":"get_transaction",
 	"params":{
         "tx_hash":"60eb029589f7fdc82118338e7513fae3bef198fd1fe3223e8506b11148858f2e"
 	}
}
```
Output:
```
{
    "jsonrpc": "2.0",
    "result": {
        "destinations": [],
        "transaction_details": {
            "address": "",
            "amount": 530002000000,
            "blockIndex": 4294967295,
            "confirmations": 0,
            "fee": 50,
            "messages": [],
            "output": true,
            "paymentId": "",
            "time": 0,
            "transactionHash": "60eb029589f7fdc82118338e7513fae3bef198fd1fe3223e8506b11148858f2e",
            "txKey": "",
            "unlockTime": 0
        }
    }
}
```


### get_tx_key

Used to get transaction secret key.

URL:
```
 /json_rpc
```
Input:
```
{
 	"jsonrpc":"2.0",
 	"method":"get_tx_key",
 	"params":{
         "tx_hash":"60eb029589f7fdc82118338e7513fae3bef198fd1fe3223e8506b11148858f2e"
 	}
}
```
Output:
```
{
    "jsonrpc": "2.0",
    "result": {
        "tx_key": "30a48e4cbf02e00e74568fbbb57ddb749671b5b651ef8714869e568f2ba03404"
    }
}
```


### get_tx_proof

Used to get payment proof to particular address.

URL:
```
 /json_rpc
```
Input:
```
{
 	"jsonrpc":"2.0",
 	"method":"get_tx_proof",
 	"params":{
         "tx_hash":"60eb029589f7fdc82118338e7513fae3bef198fd1fe3223e8506b11148858f2e",
         "tx_key": "30a48e4cbf02e00e74568fbbb57ddb749671b5b651ef8714869e568f2ba03404",
         "dest_address":"KdTf9P7ZfTDM6wfAnqGGDLE1LWEZwTVmLcGX5MPFbmRA6ce1DwuTsPPbeNiXeSamj3UjXVMGzWH5eF3HC6sRNu4NE9SGd1t"
 	}
}
```
Output:
```
{
    "jsonrpc": "2.0",
    "result": {
        "signature": "ProofQEuKv5CuAEoR69SurTBrHbfwVR5dDW2UMcsobk9PATsJsbknWwRYDuj6bXc61GDjtrAshf2yGmHWJUXhyyCeLwez1onacVS8mKxSLrna7A9dLZAkyMFWLcG4r8jskHGFe5fiVn1n4s"
    }
}
```


### query_key

Get private keys of the wallet. The `key_type` parameter may be `mnemonic` or `paperwallet`.
If the wallet is non-deterministic `mnemonic` can not be used, use `paperwallet` instead.

URL:
```
 /json_rpc
```
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "query_key",
  "params": {
      "key_type":"mnemonic"
  }
}
```
Output:
```
{
    "id": "test",
    "jsonrpc": "2.0",
    "result": {
        "key": "wrong height boyfriend amidst obvious vogue fewest object noises muppet warped initiate pigment lilac joyous hire waist anxiety swiftly enraged against fuel goblet mundane wrong"
    }
}
```


### reset

Erases simplewallet's internal state but keeps safe the wallet file. The method should be used to re-synchronize the wallet from scratch. The next refresh (which is automatically called each 20 seconds) will update the simplewallet state.

URL:
```
 /json_rpc
```
Input:
```
{
 	"jsonrpc":"2.0",
 	"method":"reset",
 	"params":{
 	}
}
```
Output:
```
{
    "jsonrpc": "2.0",
    "result": {}
}
```


### sign_message

Used to sign a *message* with wallet keys.

URL:
```
 /json_rpc
```
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "sign_message",
  "params": {
     "message": "Test"
  }
}
```
Output:
```
{
    "id": "test",
    "jsonrpc": "2.0",
    "result": {
        "signature": "SigV19QuXpiASKCJC3jsMe1GbcyNW5mj76W43U8yJXAmD5YRQnLj2KE5YGabAhbXJ69fCqcbtDaC6GN6spJzsCu3KtuQjBKqUFr"
    }
}
```


### stop_wallet

Shutdown wallet remotely.

URL:
```
 /json_rpc
```
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "stop_wallet",
  "params": {
  }
}
```
Output:
```
{
    "id": "test",
    "jsonrpc": "2.0",
    "result": {}
}
```


### store

Store wallet data.

URL:
```
  /json_rpc
```
Input: 
```
{
 	"jsonrpc": "2.0", 
 	"method": "store", 
 	"params": {}
}
```
Output:
```
{
    "jsonrpc": "2.0",
    "result": {
        "stored": true
    }
}
```


### transfer

Transfer money to several destinations with specified fee, mixin ambiguity degree, and unlock time.

Please note: fee param is a mandatory and should not be less than 0.01 in atomic units.

The `unlock_time` integer param is Unix timestamp or height.

URL:
```
 /json_rpc
```
Input:
Please note, *payment_id* is an optional argument and can be left out.
```
 {
 	"jsonrpc":"2.0",
 	"method":"transfer",
 	"params":{
 		"destinations":[
 		{
 			"amount":10000000000,
 			"address":"Kbb4JYUXJUEjPAWxuoCyVTTbtVbs32Fp22v3Kby9ziWVLJyYbqSXjadcSrHuZw91eYfQFzRtGfTemReSSMN4kE445fJGbu5"
 		},
 		{
 			"amount":210000000000,
 			"address":"KaAzzYLbBUQUG4a2b1QQVTHsDaEh7TR5UbC7HSBDZqJgFTe3CRhE6pdcSrHuZw91eYfQFzRtGfTemReSSMN4kE445gSzDQv"
 		}
 		],
 		"payment_id":"", 
 		"fee":10000000000,
		"mixin":7,
		"unlock_time":0
 	}
 }
```
Output:
```
{
    "jsonrpc": "2.0",
    "result": {
        "tx_hash": "60eb029589f7fdc82118338e7513fae3bef198fd1fe3223e8506b11148858f2e",
        "tx_key": "30a48e4cbf02e00e74568fbbb57ddb749671b5b651ef8714869e568f2ba03404"
    }
}
```


### validate_address

Check if given address is valid.

URL:
```
 /json_rpc
```
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "validate_address",
  "params": {
      "address":"LoaduyKPRsahistDfcg61udCWpEG6ghWG1qtzDmE2Zr3V7XYymSR79yMeuG1rC9myh5wVsX24MDBB8js9o5hec9yGcWohfE"
  }
}
```
Output:
```
{
    "id": "test",
    "jsonrpc": "2.0",
    "result": {
        "address": "LoaduyKPRsahistDfcg61udCWpEG6ghWG1qtzDmE2Zr3V7XYymSR79yMeuG1rC9myh5wVsX24MDBB8js9o5hec9yGcWohfE",
        "is_valid": true,
        "spend_public_key": "2e21715bd59d0ffd62e19e668e38aa9f0a416e733a39a70b72298240d4315a73",
        "status": "OK",
        "view_public_key": "7248bc700cacc6d3ea798c44c5a321e595a9fa4dfffb76935884938dc47c0d29"
    }
}
```


### verify_message

Verify signature of *message* by wallet keys.

URL:
```
 /json_rpc
```
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "verify_message",
  "params": {
     "address":"KaAzzYLbBUQUG4a2b1QQVTHsDaEh7TR5UbC7HSBDZqJgFTe3CRhE6pdcSrHuZw91eYfQFzRtGfTemReSSMN4kE445gSzDQv",
     "message": "Test",
     "signature":"SigV19QuXpiASKCJC3jsMe1GbcyNW5mj76W43U8yJXAmD5YRQnLj2KE5YGabAhbXJ69fCqcbtDaC6GN6spJzsCu3KtuQjBKqUFr"
  }
}
```
Output:
```
{
    "id": "test",
    "jsonrpc": "2.0",
    "result": {
        "good": true
    }
}
```


### estimate_fusion

Check if optimization is required.

URL:
```
 /json_rpc
```
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "estimate_fusion",
  "params": {
   "threshold":10000000000
  }
}
```
Output:
```
{
    "id": "test",
    "jsonrpc": "2.0",
    "result": {
        "fusion_ready_count": 21
    }
}
```


### send_fusion

Send fusion (optimization) transaction. It is an aggregation of small amount outputs into fever larger amounts. Fusion transaction is sent without network fee.

URL:
```
 /json_rpc
```
Input:
```
{
  "jsonrpc": "2.0",
  "id": "test",
  "method": "send_fusion",
  "params": {
   "threshold":10000000000
  }
}
```
Output:
```
{
    "id": "test",
    "jsonrpc": "2.0",
    "result": {
        "tx_hash": "7f6215897c778248ba79fb415a5cfb2a5014097d01ef3de03d75a947821a31ca"
    }
}
```
Optional parameters:
* mixin (default is 0)
* unlock_time (default is 0)