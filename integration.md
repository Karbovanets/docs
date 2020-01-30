# Integration Guide

## Overall description

We presume that blockchain will never be reorganized beyond `n_confirmations` constant, we predefine. The recommended minimum is 10 blocks as this is the maximum allowed blockchain reorganization depth in case of 51%-attack.

For services like custodial wallets and exchanges we recommend to use Payment Gateway (Karbo RPC Wallet), which is called `walletd`. The documentation for this sofware can be found here:

* [Karbo RPC Wallet JSON RPC API](walletd-json-rpc.md)
* [Karbo RPC Wallet](karbo-walletd.md)