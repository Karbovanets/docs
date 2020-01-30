
# Karbo RPC Wallet / Payment Gateway

Karbowanec RPC Wallet is a HTTP server which provides JSON 2.0 RPC interface for Karbowanec payment operations and address management. Karbowanec RPC Wallet allows you to accept incoming payments, generate an address for each user via Karbowanec RPC Wallet JSON RPC API and much more. [[RPC Wallet API]] page contains detailed description of every method. 

## Download

To start integration process you should first download Karbowanec RPC Wallet, you can find it here: https://karbo.org/download/

You may also build RPC Wallet from source code: https://github.com/seredat/karbowanec/

## Generate a new wallet

To start using RPC wallet you must first generate a container. Container file is the only file that stores all data required to run your service. It contains user addresses and private keys required to operate them. Make sure to backup this file regularly.

To generate a new container you should run the following command:

```
./walletd --container-file=<mycontainer> --container-password=<mypass> --generate-container
```

where: 
* `<mycontainer>` is the container file name and a path to it (relative or absolute); path is optional in this argument, specifying only a container's name will result in new file located in the same folder as RPC Wallet
* `<mypass>` is a secret password for the new wallet file. Whichever you like;
* `--generate-container` option tells RPC wallet to generate container file and exit.

**Note:** if `<mycontainer>` exists Karbowanec RPC Wallet will show you the notification and will ask you to provide a different name.

If the operation was successful you will get a corresponding message with your new Karbowanec address. At the same time Karbowanec RPC Wallet will save your container on the local disk (in the same folder where Karbowanec RPC Wallet is located) and shut down.

## Start Karbowanec RPC Wallet

There are two ways to start Karbowanec RPC Wallet: 

### Start with a remote connection to the Daemon 

Remote connection allows you to bind your Karbowanec RPC Wallet to a remote Karbowanec daemon (`karbowanecd`). You may establish Karbowanec daemon on both local and remote machines and connect to. Such type of connection allows you to start Karbowanec RPC Wallet on a relatively slow machine while heavy loaded daemon is going to work on a separate powerful server. 

* For local daemons use `localhost` or `127.0.0.1` as an IP address.
* For remote daemons specify the remote daemon's IP address.

Default Karbowanec daemon ports are `32347` and `32348`. 

Use the following command to start Karbowanec RPC Wallet with a remote connection: 

```
./walletd --container-file=<mycontainer> --container-password=<mypass> --daemon-address=<remote_ip> --daemon-port=32347
```

**Note:** Karbowanec daemon (`karbowanecd`) should be running at the moment RPC wallet is starting in a remote connection mode.

**Note:** Karbowanec RPC Wallet will still provide some functionality even if Daemon server fails. For example, you will be able to generate addresses for your users.

### Start as in-process node

You can also start Karbowanec RPC Wallet with an in-process node. This allows you to start RPC Wallet out-of-box with no external daemon required. You will get a fully functional node for Karbowanec network inside Karbowanec RPC Wallet. You don't have to download or install anything besides Karbowanec RPC Wallet. This approach will help reduce the overheads required for infrastructure maintenance.

Use the following command to start Karbowanec RPC Wallet with an in-process node:
```
./walletd --container-file=<mycontainer> --container-password=<mypass> --local
```

### Configure Karbowanec RPC Wallet

To configure RPC wallet you can use both command line and config file. Config file allows you to configure your settings only once and use `--config` option further. The command below launches Karbowanec RPC Wallet with a specific config file:
```
./walletd --config=~/home/Downloads/myconfig.conf
```

To get help on available options run:
```
./walletd -h
```

Please note, Karbowanec RPC Wallet config file may consist only of these options:

 Option            | Description              | Config Example     | Console Example
-------------------|--------------------------|--------------------|--------------------
`bind-address`     | Which address to bind Karbowanec RPC Wallet to. Default value is `0.0.0.0` | `bind-address = 127.0.0.1` | `--bind-address=127.0.0.1`
`bind-port`        | Which port to bind Karbowanec RPC Wallet to. Default value is `8070` | `bind-port = 8071` | `--bind-port=8071`
`daemon-address`   | Karbowanec daemon (Karbowanecd) address for remote daemon connection infrastructure | `daemon-address = 127.0.0.1` | `--daemon-address=127.0.0.1`
`daemon-port`      | Karbowanec daemon (Karbowanecd) port for remote daemon connection infrastructure. Default Karbowanec daemon ports are `32347` and `8081` | `daemon-port = 32347` | `--daemon-port=32347`
`container-file`   | **Mandatory**. Your container's file name | `container-file = mycontainer` | `--container-file=mycontainer`
`container-password` | **Mandatory**. Your container's password | `container-password = mypassword` | `--container-password=mypassword`
`log-file`         | A name of log file that you want to use for logging. Default is `walletd.log` | `log-file = mylog.log` | `--log-file=mylog.log`
`server-root`      | Working directory that you wish to use for Karbowanec RPC Wallet. Default is current working directory. | `server-root = /home/Downloads/RPCWallet` | `--server-root=/home/Downloads/RPCWallet`
`log-level`        | Level of logging. Default is 1. | `log-level = 2` | `--log-level=2`
`testnet`          | Allows you to run Karbowanec RPC Wallet in testnet. | `testnet = no` | `--testnet=no`
`local`            | Option that allows you to start Karbowanec RPC Wallet as an in-process node | `local` | `--local`
`version`          | Displays the version of the software and exits
`rpc-user`         | Username to use with the RPC server. If empty, no server authorization will be done. | `rpc-user = username` | `--rpc-user=username`
`rpc-password`     | Password to use with the RPC server. If empty, no server authorization will be done. | `rpc-password = mypassword` | `--rpc-password=mypassword`
`data-dir`         | Specify data directory | `data-dir = /home/data_dir/` | `--data-dir=/home/data_dir/`

Here's an example of a config file:
```
container-file = mycontainer
container-password = mypassword
daemon-port = 8091
bind-port = 8050
testnet = no
```

You may specify Karbowanec config directly through console arguments. Here's the same example as above in console: 
```
./walletd --container-file=mycontainer --container-password=mypassword --daemon-port=32347 --bind-port=8050 --testnet=no
```

**Note:** config file's path is relative to current working directory, not server root.

**Note:** options "container-file" and "container-password" should ALWAYS be set (in either command line or config file mode).

**Note:** "container-file" and "log-file" options are relative to "server-root". "server-root" default is the current working directory.

## Run Karbowanec RPC Wallet

Karbowanec RPC wallet can be started in both daemon and console modes. 

* **Daemon mode** - Karbowanec RPC Wallet is launched in the background, while you can continue to work with a console window. 

* **Console mode** - Karbowanec RPC Wallet is launched and prints log messages on the screen.

Karbowanec RPC wallet starts in console mode by default.

### Start as daemon (UNIX only)

To start RPC wallet as daemon just set "--daemon" (or short "-d") option.
```
./walletd --container-file=mycontainer --container-password=mypassword --daemon
```

**Note:** it's a common practice for daemons to set server root directory. 

Server root is the directory where RPC Wallet stores all its files. All relative paths in RPC Wallet configuration are relative to the server root directory.

### Start as service (Windows only)

To run RPC wallet as a service on Windows you have to do the following:

1. Create a config file and place it in the same directory as your RPC wallet's executable resides in. 

A note for Windows Users: In case the server root in config file is not specified all paths should be ABSOLUTE. If you set server root you can use relative paths (relative to your server root);

2. Register your Karbowanec RPC Wallet as a service. To do so, run the following command as an ADMINISTRATOR:
```
walletd.exe --register-service
```

3. After you see message about successful service registration you can run it in your Services panel.

### Uninstall service (Windows only)

If you want to delete RPC wallet you have to unregister windows service first (if you have registered it before). Run as an ADMINISTRATOR:
```
walletd.exe --unregister-service
```

## RPC Wallet JSON RPC API

Karbowanec RPC Wallet API allows you to create addresses for your users, accept and send transactions and much more. 

Detailed description for every Karbowanec RPC Wallet API method can be found here: [RPC Wallet API](walletd-json-rpc.md)
