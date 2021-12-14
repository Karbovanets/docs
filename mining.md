# Solo mining

For solo mining you will need either Karbo Command Line Suite or GUI wallet.

You will also need wallet to where mined coins will be received. You can use GUI wallet, web-wallet, simplewallet (which is bundled with CLI daemon) or even paperwallet to generate wallet keys.

**Note:** For Karbo solo mining you need not just wallet address but its secret keys.


## GUI Wallet

Download and install Karbo GUI Wallet Classic, create or open wallet, head to `Mining` tab and hit the button `Start Mining`. That's all. You can play around with CPU cores but don't set it to maximum as at some point it will stop enlarging your hashrate.


## Command line

You can start solo mining in few different ways.

Presuming you downloaded and unpacked Command Line Suite and you have wallet keys, you can start mining. You will need both `Secret Spend Key` and `Secret View Key` in form of 64-character hex strings.

**WARNING! Be aware that anyone who can see these mining commands will have access to your wallet as they reveal keys to wallet in plain text! Make sure you have safe environment for mining.**

### Option 1: mining in daemon with command

Run daemon named `karbowanecd`. Wait for it to finish synchronization. Then type 
```
start_mining SECRET_SPEND_KEY SECRET_VIEW_KEY [threads=1]
```

The first parameter is your `Secret Spend Key`, the second is `Secret View Key`, the third, optional, is the number of CPU cores, which you want to use for mining, default is 1. 

*Note*: There is no need to enter maximum available number of cores, because it not necessarily will give maximal hashrate. See which number gives you the best results.

Example: 
```
start_mining 1a0b4a1b42d234ddd57dadd34baa7b6e7d34d8be6a795bee0ab2215e7b3201b7 bce354c4c6b5035b946e60acb116dbd038c2c2f3cb005a79c4dbe1af430e597a 2
```

Type `show_hr` to see the hashrate. To stop displaying hashrate type `hide_hr`.

To stop mining type `stop_mining`.

### Option 2: mining in daemon on startup

If you run Karbo daemon with special startup flags it will start mining automatically upon finishing synchronization. These are `--mining-spend-key`, `--mining-view-key`, `--mining-threads`.

Example:
```
./karbowanecd --mining-spend-key 1a0b4a1b42d234ddd57dadd34baa7b6e7d34d8be6a795bee0ab2215e7b3201b7 --mining-view-key bce354c4c6b5035b946e60acb116dbd038c2c2f3cb005a79c4dbe1af430e597a --mining-threads 2
```

### Option 3: mining in daemon from simplewallet

You can also run solo mining from `simplewallet`.

First, run daemon and make sure it is synchronized. Then in another terminal run `simplewallet`, generate new or open existing wallet and enter command `start_mining [<number_of_threads>]`. The daemon will start mining to this wallet.
