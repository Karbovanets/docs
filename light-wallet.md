# Light Wallet & Masternodes

## Light wallet

It is possible to use wallet without blockchain, in remote mode it will be connected to the remote node. This allows to get fully functional wallet faster.

Just select remote node in settings and restart wallet if you're using GUI, or run **simplewallet** from CLI suite with `--daemon-address` or `--daemon-host` and `--daemon-port` flags. It is quite safe, the node can't steal your coins.
			

If you enter *node.karbowanec.com* or *node.karbo.io* or *node.karbo.org* you will be connected to random public node, so-called *'masternode'* launched by community members. The list of available masternodes can be found for example at [map.karbo.xyz](http://map.karbo.xyz/masternodes) or at Karbo blockchain explorers.


## Masternodes for lite wallets

Cryptonote coin's wallets can operate through remote daemon without downloading blockchain. It allows to start working quickly when needed. It is quite safe as remote daemon can't steal your coins, running own node is more secure of course. To work through remote daemon in **simplewallet** you need to specify remote daemon's address with flag for example `--daemon-address=136.243.158.27:32348`, in GUI you can just select remote node in settings or add custom one. But these remote nodes are not rewarded anyhow in any CN coin. Only in Karbo such remote nodes are rewarded for their service. We call them Masternodes because this term is well known.

So, basically, masternode it is the CLI Karbo daemon running on a machine with open port which allows to connect to it for such light wallets and mobile wallets. Karbo wallets, connected to masternode, are paying small fees to that node when are sending transactions through it. These fees are supposed to help to cover the costs of operating Karbo nodes.


## Running a public node

To start own Karbowanec masternode all is needed is just a machine with static IP and open port. Machine should have enough CPU power to handle load when parsing blockchain for connected wallets, it can be even spare PC at home. On such machine you can run Karbo daemon specifying a wallet address where fees would go like this:
			
```
./karbowanecd --restricted-rpc --enable-cors=*  --enable-blockchain-indexes --rpc-bind-ip=0.0.0.0 --rpc-bind-port=32348
--fee-address=KaqCQAbx3BSKKv7ED98oQP9QSP3igqgo47hPYZ8q6KZyUY6GnDaQkh9WbVR4DxvmCq8mZcKPg3wfWFJQ5CsyrxPqKcXC3rx
```
			
You can specify any wallet address, it can be your GUI wallet address, even paper wallet. This is the wallet where you will receive fees.</p>
			
You need to make sure your port is open and not blocked by firewall. If you are running it at home behind router you need to do port forwarding.</p>

If you have PC at home constantly running with fast connection and static IP and  want to operate such masternode to help Karbo network, run daemon as in example and publish you IP on community forums or chats so users can find it.</p>
			
You can check if your node is running opening its IP in browser like this:
```
http://185.51.246.81:32348/feeaddress
```
and you should see something like this:
```
{"fee_address":"KhjM2KE6CXnDqERpSQckdgaT1VcpPuqxKavZwLxYwtqs4j3eWCVE9MtEV4xxdQVp13V4NYMRWbQqYG9jRw5XNkRUKLjfHwR","status":"OK"}
```
with your wallet address where fees should go.

You can also run masternode on VPS with dedicated domain and publish it with description so people can add your node manually if they prefer it. It is not recommended to run node on VPS now specially for Karbo, do it only when you already have spare VPS and it is idling.

Do not expect yet to earn a lot of fees. This is not for-profit but rather a way to help and support the network.