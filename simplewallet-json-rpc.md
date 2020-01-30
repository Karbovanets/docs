To start wallet JSON RPC API server you should specify a port on which server binds (additionally to standard wallet's arguments). You can choose any free port. To do that execute the following command from the command line:
```
 simplewallet --wallet-file=example_wallet.bin --pass=12345 '''--rpc-bind-port=32348'''
```
Having done that you're ready to operate with the wallet through the following API URLs (e.g., your IP address is 95.46.98.64):

 http://95.46.98.64:32348/json_rpc
 http://localhost:32348/json_rpc

## Available commands ##

* getbalance
* transfer
* store
* get_payments
* get_transfers
* get_height
* reset

Please note, there is no "refresh" RPC method. RPC wallet refresh is performed automatically each 20 seconds.


### getbalance ###

Return balance.

URL:
```
 /json_rpc
```
Input: 
```
 {
 	"$schema": "http://json-schema.org/draft-04/schema#",
 	"title": "Karbowanec wallet api",
 	"description": "Schema for transfer method in Karbowanec wallet",
 	"type": "object", 
 	
 	"properties" : {
 		"jsonrpc" : {
 			"type" : "string"
 		}, 
 		"method" : {
 			"type" : "string"
 		}
 	}
 }
```
Output:
```
 {
 	"$schema": "http://json-schema.org/draft-04/schema#",
 	"title": "Karbowanec wallet api",
 	"description": "Schema for transfer method in Karbowanec wallet",
 	"type": "object",
 	
 	"properties" : {
 		"locked_amount" : {
 			"type" : "integer"
 		},
 		"available_balance" : {
 			"type" : "integer"
 		}
 	}
 }
```

### transfer ###

Transfer money to several destinations with specified fee, mixin ambiguity degree, and unlock time.

Please note: fee param is a mandatory and should not be less than 0.01 BCN

URL:
```
 /json_rpc
```
Input:
```
 {
 	"$schema": "http://json-schema.org/draft-04/schema#",
 	"title": "Karbowanec wallet api",
 	"description": "Schema for transfer method in Karbowanec wallet",
 	"type": "object",
 	
 	"properties" : {
 		"jsonrpc" : {
 			"type" : "string"
 		}, 
 		"method" : {
 			"type" : "string"
 		},
 		"destinations" : {
 			"type" : "array",
 			"items" : {
 				"amount" : {
 					"type" : "integer"
 				},
 				"address" : {
 					"type" : "string"
 				}
 			},
 			"minItems" : 1
 		},
 
 		"payment_id": {
 			"type" : "string"
 		}
 	
 		"fee" : {
 			"type" : "integer"
 		},
 		
 		"mixin" : {
 			"type" : "integer"
 		},
 		
 		"unlock_time" : { 
 			"type" : "integer"
 			"description" : "Unix timestamp"
 		}
 	}
 }
```
Output:
```
 {
 	"$schema": "http://json-schema.org/draft-04/schema#",
 	"title": "Karbowanec wallet api",
 	"description": "Schema for transfer method in Karbowanec wallet",
 	"type": "object",
 	
 	"properties" : {
 		"tx_hash" : {
 			"type" : "string"
 		}
 	}
 }
```
### store ###

Store wallet data.

URL:
```
  /json_rpc
```
Input: 
```
 {
 	"$schema": "http://json-schema.org/draft-04/schema#",
 	"title": "Karbowanec wallet api",
 	"description": "Schema for transfer method in Karbowanec wallet",
 	"type": "object",
 	
 	"properties" : {
 		"jsonrpc" : {
 			"type" : "string"
 		}, 
 		"method" : {
 			"type" : "string"
 		}
 	}
 }
```
Output: 
```
 {
 	"$schema": "http://json-schema.org/draft-04/schema#",
 	"title": "Karbowanec wallet api",
 	"description": "Schema for transfer method in Karbowanec wallet",
 	"type": "object",
 	
 	"properties" : {}
 }
```
### get_payments ###

Receives all the payments with a corresponding payment_id that were sent to the wallet. This method is used to get the BCN payments for the 3rd party services. As Karbowanec uses only one address to receive BCN deposits, a unique payment_id should be assigned and shown to each user. The method will return all the payments for this user.

URL:
```
 /json_rpc
```
Input: 
```
 {
 	"$schema": "http://json-schema.org/draft-04/schema#",
 	"title": "Karbowanec wallet api",
 	"description": "Schema for transfer method in Karbowanec wallet",
 	"type": "object", 
 
 	"properties" : {
 		"jsonrpc" : {
 			"type" : "string"
 		}, 
 		"method" : {
 			"type" : "string"
 		},
 
 		"payment_id" :  {
 			"type" : "string"
 		}
 	}
 }
```
Output: 
```
 {
 	"$schema": "http://json-schema.org/draft-04/schema#",
 	"title": "Karbowanec wallet api",
 	"description": "Schema for transfer method in Karbowanec wallet",
 	"type": "object",
 
 	"properties" : {
 		"payments" : {
 			"type" : "array",
 			"items" : {
 				"amount" : {
 					"type" : "integer"
 				},
 				"block_height" : {
 					"type" : "integer"
 				},
 				"tx_hash" : {
 					"type" : "string"
 				},
 				"unlock_time" : {
 					"type" : "integer"
 				}
 			}
 		}
 	}
 }
```
### get_transfers ###

Returns the list of all the wallet's incoming and outgoing transfers. This data is available starting from v.1.0.2 build. For the transfers created by simplewallet of previous versions this method returns not exact transfers amounts but the transaction amounts (transfer amount + change).

URL: 
```
 /json_rpc
```
Input:
```
 {
 	"$schema": "http://json-schema.org/draft-04/schema#",
 	"title": "Karbowanec wallet api",
 	"description": "Schema for transfer method in Karbowanec wallet",
 	"type": "object",
 	
 	"properties" : {
 		"jsonrpc" : {
 			"type" : "string"
 		}, 
 		"method" : {
 			"type" : "string"
 		}
 	}
 }
```
Output:
```
 {
 	"$schema": "http://json-schema.org/draft-04/schema#",
 	"title": "Karbowanec wallet api",
 	"description": "Schema for transfer method in Karbowanec wallet",
 	"type": "object",
 
 	"properties" : {
 		"result" : {
 			"type" : "transfers"
 			"transfers" : {
 				"type" : "array",
 				"items" : {
 					"address" : {
 						"type" : "string"
 					},
 					"amount" : {
 						"type" : "integer"
 					},
 					"blockIndex" : {
 						"type" : "integer"
 					},
 					"fee" : {
 						"type" : "integer"
 					},
 					"output" : {
 						"type" : "boolean"
 					},
 					"paymentId" : {
 						"type" : "string"
 					},
 					"time" : {
 						"type" : "integer"
 					},
 					"transactionHash" : {
 						"type" : "string"
 					},
 					"unlockTime" : {
 						"type" : "integer"
 					},
 				}				
 			}				
 		}
 	}
 }
```
### get_height ###

Returns the last top known block height for simplewallet. This method can be used to verify that simplewallet is correctly synchronized.

URL:
```
 /json_rpc
```
Input:
```
 {
 	"$schema": "http://json-schema.org/draft-04/schema#",
 	"title": "Karbowanec wallet api",
 	"description": "Schema for transfer method in Karbowanec wallet",
 	"type": "object",
 	
 	"properties" : {
 		"jsonrpc" : {
 			"type" : "string"
 		}, 
 		"method" : {
 			"type" : "string"
 		}
 	}
 }
```
Output:
```
 {
 	"$schema": "http://json-schema.org/draft-04/schema#",
 	"title": "Karbowanec wallet api",
 	"description": "Schema for transfer method in Karbowanec wallet",
 	"type": "object",
 	
 	"properties" : {
 		"height" : {
 			"type" : "integer"
 		}
 	}
 }
```
### reset ###

Erases simplewallet's internal state but keeps safe the wallet.bin. The method should be used to re-synchronize the wallet from scratch. The next refresh (which is automatically called each 20 seconds) will update the simplewallet state.

URL:
```
 /json_rpc
```
Input:
```
 {
 	"$schema": "http://json-schema.org/draft-04/schema#",
 	"title": "Karbowanec wallet api",
 	"description": "Schema for transfer method in Karbowanec wallet",
 	"type": "object",
 	
 	"properties" : {
 		"jsonrpc" : {
 			"type" : "string"
 		}, 
 		"method" : {
 			"type" : "string"
 		}
 	}
 }
```
Output:
```
 {
 	"$schema": "http://json-schema.org/draft-04/schema#",
 	"title": "Karbowanec wallet api",
 	"description": "Schema for transfer method in Karbowanec wallet",
 	"type": "object",
 	
 	"properties" : {}
 }
```

## Examples ##

### getbalance ###
```
 {
 	"jsonrpc": "2.0", 
 	"method": "getbalance", 
 	"params": {}
 }
```
### transfer ###

Please note, payment_id is an optional argument and can be left out.
```
 {
 	"jsonrpc":"2.0",
 	"method":"transfer",
 	"params":{
 		"destinations":[
 		{
 			"amount":11111,
 			"address":"KfXkT5VmdqmA7bWqSH37p87hSXBdTpTogN4mGHPARUSJaLse6jbXaVbVkLs3DwcmuD88xfu835Zvh6qBPCUXw6CHK8koDCt"
 		},
 		{
 			"amount":22222,
 			"address":"KfXkT5VmdqmA7bWqSH37p87hSXBdTpTogN4mGHPARUSJaLse6jbXaVbVkLs3DwcmuD88xfu835Zvh6qBPCUXw6CHK8koDCt"
 		}
 		],
 		"payment_id":"", 
 		"fee":1000000,
 		"mixin":0,
 		"unlock_time":0
 	}
 }
```
### store ###
```
 {
 	"jsonrpc": "2.0", 
 	"method": "store", 
 	"params": {}
 }
```
### get_payments ###
```
 {
 	"jsonrpc":"2.0",
 	"method":"get_payments",
 	"params":{
 		"payment_id": "78cc4b76a48bd50ab955ac61a0c04e4a82079fbcf27298f87b39c76aefccbcc9"
 	}
 }
```
### get_transfers ###
```
 {
 	"jsonrpc": "2.0", 
 	"method": "get_transfers", 
 	"params": {}
 }
```
### get_height ###
```
 {
 	"jsonrpc": "2.0", 
 	"method": "get_height", 
 	"params": {}
 }
```
### reset ###
```
 {
 	"jsonrpc": "2.0", 
 	"method": "reset", 
 	"params": {}
 }
```
