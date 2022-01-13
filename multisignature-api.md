#Multisignature API

Currently Karbo implements standard M—N multisigs through ITransaction low-level API.

Multisignature is a special type of output destination address in a transaction. Usually every output is sent to one public key, which belongs to a single person, but multi-signatures allow you to create a “virtual address” in such a way that many people can (and should) cooperate to release the money associated with that address.

The Multi-signature features are best shown in the following example:

Let’s assume you want to send your funds to the CryptoNote Foundation. There are 3 core members in the foundation so you set the number of signatures that will be needed for the transaction spending to 2. Mine or buy an amount you want to send and create a transaction with 3 addresses of the Board Members. For the sake of convenience we’ll call these addresses - “consilium”. Business communications of the Board members are done through 3rd party software that allows holding a discussion and has the ability to show all the transactions that are sent to the members.

`sendAmount = your.balance`

```
input[0] = type:InputKey, amount:sendAmount
output[1] = type:OutputMultisignature, amount:sendAmount-fee, to = consilium
```

Through their 3rd party software every “consilium” member should receive a notification about the incoming multi-signature transaction. Then they decide which product or service they want to spend their money on. As soon as the decision is made they can start a transaction signing process. The process is very simple - one of the Board members verifies a transaction, signs it and then sends it to two other members via 3rd party software.

```
// SIGNING CODE

std::unique_ptr<ITransaction> tx = createTransaction(transactionBlob);

TransactionTypes::InputMultisignature input;
TransactionTypes::OutputKey output;

tx->getInput(0, input);
tx->getOutput(0, output);

// verify inputs & outputs
if (input.amount != sendAmount + fee) {
   // error
}

if (output.amount != sendAmount) {
  // wrong output amount
}

// add signature
// signer must know source transaction public key and output index
tx->signInputMultisignature(0, transactionPublicKey, outputInTransaction, memberKeys);
auto signedTx = tx->getTransactionData();

// send signedTx to other member
```

The other two members must verify the transaction to make sure nothing was changed, e.g. transaction parameters (amount & destination) was not substituted and that it was indeed signed by the first member of the Board.

```
// VERIFYING CODE

std::unique_ptr<ITransaction> tx = createTransaction(signedTx);

TransactionTypes::InputMultisignature input;
TransactionTypes::OutputKey output;

tx->getInput(0, input);
tx->getOutput(0, output);

// verify inputs & outputs
...

// check if we have enough signatures
bool isValid = tx->validateSignatures();
```

As soon as verification is done, one of the members signs the transaction with the code presented above. This transaction now can be sent to the network and funds should be available for spending in due time.

There surely will be cases where the Board Members will not spend the whole sum at once and will have to send a change back. In this particular occasion the Board Members should repeat the process from the beginning, i.e. send a transaction to the Board Member addresses, sign it and send it to the network. 