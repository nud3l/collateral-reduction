# Ecosystem-wide Secure Collateral Reduction

We propose a generalized mechanism for a reduction of collateral in the Ethereum space. The idea builds on the [Balance paper](https://eprint.iacr.org/2019/675.pdf) and uses it as the core mechanism. 
The proposal is a response to Problem 12 in [Hard Problems in Cryptocurrencies](https://github.com/ethereum/wiki/wiki/Problems#12-reputation-systems).

## Reputation in Blockchains

Reputation in decentralized and permissionless systems must be different from other systems that have some notion of inherent trust.
We cannot rely on a trusted third-party to maintain a list of a reputation of different agents in a system.
Further, we cannot rely on strong identities and, on purpose, must tolerate Sybil identities.

## Open Problems for Reputation Sytems

Problem 12 in [Hard Problems in Cryptocurrencies](https://github.com/ethereum/wiki/wiki/Problems#12-reputation-systems) lists four distinct sub-problems.
We address these problems with our system.

1. Single-shot attacks in reputation: an agent can act honestly for a  number of rounds and when trusted enough, acts maliciously.
2. Reputation boosting: an agent can boost its reputation by creating Sybil identities through which it interacts with itself to increase its reputation. Other agents might rely on that boosted reputation and might be cheated on.
3. Explicit vs implicit reputation: if reputation is expressed as something that is obtainable, i.e. on an open market, agents might be motivated to sell and buy reputation. For example, Alice and Bob can make an agreement to rate each other positively.
4. Compositional trust: Alice might be under-collateralized when dealing with multiple agents. For example, Alice might have a deposit of 2 ETH and uses this deposit to interact with five agents with a risk of 1 ETH each. The five agents might not be aware of each other. If Alice is able to gain 5 ETH from being malicious, it would be individually rational for her to take the 2 ETH damage and gain the 5 ETH.

## Introducing YATS

YATS (Yet Another Trust System) is supposed to be implemented as a smart contract on top of Ethereum.
Its basic functionality is equal to the one introduced in [Balance](balance-resear.ch).

### Registry of Agents

YATS keeps track of actions of agents via a registry.
An agent can have one more identities, where each public key represents an identity.
When an agent is registered with YATS at least one of its public keys is associated with a "ranking" in the registry.


