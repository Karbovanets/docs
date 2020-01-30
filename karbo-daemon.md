# Daemon command line arguments and commands


## Command line options

Option                                 | Description
-------------------------------------- | -----------------------------
  `--help`                             | Produce help message
  `--version`                          | Output version information
  `--os-version`                       |
  `--data-dir arg`                     | Specify data directory
  `--config-file arg`                  | Specify configuration file

## Command line options and settings options

Option                                 | Description
-------------------------------------- | -----------------------------
  `--log-file arg`                     |
  `--log-level arg (=0)`               |
  `--no-console`                       | Disable daemon console commands
  `--testnet`                          | Used to deploy test nets. Checkpoints and hardcoded seeds are ignored, network id is changed. Use it with --data-dir flag. The wallet must be launched with --testnet flag.
  `--rpc-bind-ip arg (=127.0.0.1)`     |
  `--rpc-bind-port arg (=32348)`       |
  `--p2p-bind-ip arg (=0.0.0.0)`       | Interface for p2p network protocol
  `--p2p-bind-port arg (=32347)`       |  Port for p2p network protocol
  `--p2p-external-port arg (=0)`       | External port for p2p network protocol (if port forwarding used with NAT)
  `--allow-local-ip`                   | Allow local ip add to peer list, mostly in debug purposes
  `--add-peer arg`                     | Manually add peer to local peerlist
  `--add-priority-node arg`            | With this parameter(s) could be set list peers to connect to and attempt to keep the connection open
  `--seed-node arg`                    | Connect to a node to retrieve peer addresses, and disconnect
  `--add-exclusive-node arg`           | Specify list of peers to connect to only. If this option is given the options add-priority-node and seed-node are ignored
  `--hide-my-port`                     | Do not announce yourself as peerlist candidate
  `--extra-messages-file arg`          | Specify file for extra messages to include into coinbase transactions
  `--start-mining arg`                 | Specify wallet address to mine for
  `--mining-threads arg`               | Specify mining threads count


## Daemon commands

Command                   | Description                   | Arg 1                  | Arg 2    
--------------------------|-------------------------------|------------------------|------------------------
 `help`                   | Print available commands      | -                      | -
 `start_mining`           | Start mining in several threads to a given wallet address | [string] wallet_address | [uint] threads
 `stop_mining`            | Stop mining
 `show_hr`                | Show current mining hashrate
 `hide_hr`                | Stop showing current mining hashrate
 `exit`                   | Exit karbowanecd
 `ban`                    | Ban a given <IP> for a given amount of <seconds> | [string] IP_address | [uint] seconds
 `unban`                  | Unban a given <IP>            | [string] IP_address
 `height`                 | Print current blockchain height
 `print_bc`               | Print blockchain info in a given blocks range | [uint] begin_height | [uint] end_height (optional)
 `print_block`            | Print block                   | [string] block_hash or [uint] block_height
 `print_cn`               | Print connections
 `print_diff`             | Print difficulty for the next block
 `print_pl`               | Print peer list
 `print_pool`             | Print transaction pool (long format)
 `print_pool_sh`          | Print transaction pool (short format)
 `print_mp`               | Print number of transactions in memory pool
 `print_tx`               | Print transaction             | [string] transaction_hash
 `set_log`                | Change current log detailization level | [uint] log level (0 - 4)
 `status`                 | Print information about blockchain and daemon status
 `save`                   | Store blockchain data to disk

