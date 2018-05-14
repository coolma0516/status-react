# 0003. Geth node for Beta

| Date | Tags |
|---|---|
| 2018-05-14 | architecture, p2p, scope   |


## Status

proposed

## Context

On the path to releasing a usable beta we've faced a variety of performance
issues (https://github.com/status-im/ideas/issues/55,
https://ideas.status.im/ideas/071-low-traffic,
https://ideas.status.im/ideas/076-smooth-ui,
https://ideas.status.im/ideas/083-energy-efficient).

Some of these performance issues are related to the use of LES, especially on
Mainnet. Examples of problems include: slow/hot sync, disk filling up, bandwidth
usage, etc. This can partly be remedied by the use of CHT to speed up sync
(https://github.com/status-im/status-go/wiki/Updating-CHT-BloomTrie).

In order to simplify the problem, we decided earlier this year to not spend too
much time looking into performance improvements related to LES, instead focusing
our efforts on improving the performance on Whisper and in client-side code.

This also means we don't have a full picture of to what extent LES is a
performance bottleneck for the Status app. It is possible proper use of CHT,
slowing sync down, vary load depending on if you are on WiFi or not, etc, can
solve these problems. However, the consensus right now is that ULC is the more
promising route to take.

However, this means we are relying on Infura, which is a bad idea from a
decentralization and security point of view. This can be partly remedied by
allowing the user to run an upstream node. It is still a bad trust model,
relying on third-party Ethereum nodes, and we want to get away from this as
soon as possible.

## Decision

1. RELY ON UPSTREAM NODES. For the closed beta scheduled to be releases Q2 we
will provide two ways of accessing the Ethereum network:

- Upstream RPC with Infura (default)
- Custom upstream node (https://github.com/status-im/status-react/issues/3994)

From a decentralization point of view we need the latter before we can release
the beta.

2. ULC MVP. Additionally, as soon as beta is released, assess and start to
   introduce ULC as an experimental non-default mode in the app.
   
By doing this we also support the network, since it is still a very new protocol>

3. (OPTIONAL) LES TRACK. If we still have resources and there's interest,
optionally run a parallel track to clean up LES usage (update CHT, cluster) and
understand exact performance impact and viablity of running LES on
resource-constrained devices.

These three decisions balances the following trade-offs:

- get a usable beta released as soon as possible
- provide users with options to get minimal amount of decentralization
- pave the way for trustless usage by default (ULC/LES node)

## Consequences

Most of this is captured above.

- Make sure custom upstream RPC is in beta and works
- Continue work on https://github.com/status-im/ideas/pull/254/files, consider
  adding more resources to get it into MVP state as soon as possible
