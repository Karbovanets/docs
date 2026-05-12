# Deep Reorg Protection for Karbo Public Infrastructure

## Motivation

Karbo uses Signed Proof of Work with Blockchain cache scratchpad to keep mining closer to real solo miners and make conventional pool mining difficult. This improves decentralization, but it does not fully remove the risk that one large solo miner with enough hardware could temporarily control the majority of hashrate.

For a small proof-of-work network, the main danger is not only that such a miner can produce many new blocks. The more serious danger is a deep reorganization: a late-arriving alternative chain that rewrites many already-confirmed blocks. This can be used to reverse deposits, confuse wallets and explorers, or damage trust in the network.

Karbo already has a simple and practical defense against this: official, public, explorer, and exchange nodes can run with *deep reorg rejection enabled*.

```
--reject-deep-reorg
```


## Nakamoto Consensus Near the Tip

Karbo should still follow normal Nakamoto consensus near the chain tip.

Short reorganizations are a natural part of proof-of-work. Two miners may find blocks close together, some nodes may see one block first, and the network eventually converges on the chain with the most accumulated work.

This behavior should remain unchanged for shallow reorgs.

The purpose of deep reorg protection is not to replace proof-of-work. It is to define a safety boundary after which public infrastructure refuses to automatically rewrite history.

## First-Seen Public Chain After Finality

After a block is buried deeper than the configured finality depth, public and service-grade nodes should preserve the first-seen public chain.

This means:

```text
Near the tip: follow normal proof-of-work consensus.
After finality depth: keep the first-seen finalized public chain.
```

A late deep alternative chain should not automatically replace the public chain, even if it has more accumulated work.

This is important because a deep alternative chain is not necessarily a valid public continuation of the network. It may come from:

- a private 51% attack;
- an isolated miner stuck on an alternative chain;
- a network partition;
- poor peer connectivity;
- a node or firewall problem;
- delayed communication between parts of the network.

In those cases, the first-seen public chain followed by official nodes, explorers, exchanges, and public RPC infrastructure is most likely the valid chain from the point of view of users and services. The isolated or late-arriving branch should reorg back to the public chain, not force the public ecosystem to rewrite already-finalized history.

## Practical Trailing Finality

Deep reorg rejection acts like a trailing checkpoint, but without requiring masternodes, stake voting, slashing, or a validator set.

Example:

```text
Current height: 1,500,000
Maximum accepted reorg depth: 10
Finalized height: 1,499,990
```

The node may still reorganize the most recent 10 blocks. But it will reject a fork that tries to replace block 1,499,990 or earlier.

This gives Karbo practical trailing finality:

- normal proof-of-work remains active near the tip;
- natural short reorgs remain possible;
- deep history is protected from automatic rewrites;
- exchanges and explorers gain a clear safety rule.

## Public Infrastructure Priority Peer Mesh

Deep reorg protection works best when official and public infrastructure nodes see the same public chain quickly. For this reason, official nodes, explorers, public RPC nodes, and exchange-facing nodes should add each other as priority peers.

In Karbo, priority peers are a networking feature, not a consensus-trust feature. The `--add-priority-node` option tells the node to connect to the specified peer and attempt to keep that connection open. Priority peers improve connectivity and block propagation between important public nodes.

They do not:

- bypass block or transaction validation;
- override proof-of-work consensus near the tip;
- override deep reorg rejection;
- act as signed checkpoints;
- make the node trust blocks from those peers automatically.

This makes priority peers suitable for building a public infrastructure mesh:

```text
official node A <-> official node B
official node A <-> explorer
official node B <-> public RPC node
explorer <-> exchange-facing node
```

The purpose is to ensure that the first-seen public chain is actually common ground between public services. If official nodes, explorers, RPC nodes, and exchanges are well connected to each other, they are more likely to see the same blocks early and finalize the same chain after the configured finality depth.

This should not be confused with exclusive peering. Karbo also supports exclusive nodes, but exclusive mode connects only to the specified peers and ignores normal seed or priority peer behavior. That is not recommended for public infrastructure under normal conditions.

Public nodes should keep normal peer discovery and random peer connectivity enabled. Priority peers should supplement the normal network, not replace it.

Recommended operating policy:

```text
Enable deep reorg protection.
Add other known public infrastructure nodes as priority peers.
Keep normal peer discovery enabled.
Do not use exclusive nodes for normal public operation.
Use enough total connections so priority peers do not crowd out ordinary peers.
Monitor priority peer connectivity and public-node chain agreement.
```

Example configuration:

```text
--reject-deep-reorg=10
--connections=24
--add-priority-node node1.karbo.org:32348
--add-priority-node node2.karbo.org:32348
--add-priority-node explorer.karbo.org:32348
```

In short:

```text
Priority peers improve propagation.
They do not define consensus.
They help public nodes share the same first-seen public chain.
```

## Who Should Enable It

Deep reorg protection is recommended for:

- official Karbo nodes;
- public RPC nodes;
- block explorers;
- exchange nodes;
- wallet backend nodes;
- payment processors;
- other public infrastructure providers.

These nodes serve users and services. Their priority should be stable public history, not automatically following every late deep fork.

Solo miners and private nodes may choose their own policy, but public infrastructure should use a consistent finality rule.

## Exchange and Explorer Policy

Exchanges are the most likely target of deep reorg attacks. Exchange nodes should reject deep reorgs and require deposit confirmations at or beyond the configured finality depth.

Explorers should also run with deep reorg protection because users often treat the explorer as the public reference for chain history.

A useful public status display would include:

```json
{
  "deep_reorg_protection": true,
  "max_reorg_depth": 10,
  "finalized_height": 1499990,
  "finalized_hash": "..."
}
```

This makes the node's finality policy transparent and easy for services to monitor.

## Tradeoff

Deep reorg protection is a conscious tradeoff.

Pure Nakamoto consensus says a node should follow the valid chain with the most accumulated work. Deep reorg protection says this is true only within the allowed reorg window. After finality depth, public nodes preserve the first-seen finalized public chain.

For a large proof-of-work network, deep reorgs are extremely expensive. For a small proof-of-work network, deep reorgs are realistic enough that automatic acceptance can be dangerous.

Karbo should prioritize public-chain stability for users, exchanges, wallets, and explorers.

## Conclusion

Deep reorg rejection is a simple, practical safety layer for Karbo.

It does not replace proof-of-work. It does not require masternodes. It does not turn Karbo into a proof-of-stake or validator-governed system.

It simply means that official and service-grade nodes follow Nakamoto consensus near the tip, but protect already-finalized public history from late deep rewrites.

The recommended policy is:

```text
Follow proof-of-work near the tip.
Reject deep reorgs beyond the configured finality depth.
Preserve the first-seen finalized public chain.
Treat late deep forks as suspicious or isolated unless manually reviewed.
```

This gives Karbo a practical defense against deep 51% reorgs while preserving its proof-of-work identity.
