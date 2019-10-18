# Secure Collateral Reduction for Many Protocols

In decentralized ledger, we replace trust by deposits. This is a requirement to decouple our different identities in various protocol.
For example, I might want to use several public keys to interact in various protocol.
Any decentrlaized protocol should further not require a party to go through a KYC process.
Doing so, removes the decentralized aspect as we need a trusted third party to attest to the correctness of the KYC process.

In practice, protocols use collateral instead. For example, Dai creates a soft-peg to the USD maintained by agents that open CDPs.
Those agents are expected to maintain their required level of collateral or so-called Keepers will step in and liquidate their CDP.
Further, Proof-of-Stake (PoS) protocols build on the very notion that we can motivate validators to behave honestly by (1) threatening to destroy their deposit if they cheat and (2) paying them a reward for acting honestly.

Using deposits as a means of trust is quite inefficient though:
In most cases it is impossible to determine the exact amount of required collateral.
This is caused by the fact that collateral is typically provided for a period of time in which e.g. the valuation of a currency fluctuates.
Moreover, other agents in the system might have hidden motivations, e.g. they are bribed to behave a certain way.
As a response, protocol require over-collateralization.
Without over-collateraliation, protocols are prone to the event-dependency and private information based security issues.

To lower the burden of over-collateralization, we propose a generalized mechanism for a reduction of collateral in a range of protocols. 
Suitable protocols for our mechanism have the following properties:

- Require deposits to protect against rational adversaries
- Require over-collateralization
- Eventual decision finality

The idea builds on the [Balance paper](https://eprint.iacr.org/2019/675.pdf) and uses it as the core mechanism. 
The proposal is a response to Problem 12 in [Hard Problems in Cryptocurrencies](https://github.com/ethereum/wiki/wiki/Problems#12-reputation-systems).

## Reputation in Blockchains

Reputation in decentralized and permissionless systems must be different from other systems that have some notion of inherent trust.
We cannot rely on a trusted third-party to maintain a list of a reputation of different agents in a system.
Further, we cannot rely on strong identities and, on purpose, must tolerate Sybil identities.

Problem 12 in [Hard Problems in Cryptocurrencies](https://github.com/ethereum/wiki/wiki/Problems#12-reputation-systems) lists four distinct sub-problems.
We address these problems with our system.

1. Single-shot attacks in reputation: an agent can act honestly for a  number of rounds and when trusted enough, acts maliciously.
2. Reputation boosting: an agent can boost its reputation by creating Sybil identities through which it interacts with itself to increase its reputation. Other agents might rely on that boosted reputation and might be cheated on.
3. Explicit vs implicit reputation: if reputation is expressed as something that is obtainable, i.e. on an open market, agents might be motivated to sell and buy reputation. For example, Alice and Bob can make an agreement to rate each other positively.
4. Compositional trust: Alice might be under-collateralized when dealing with multiple agents. For example, Alice might have a deposit of 2 ETH and uses this deposit to interact with five agents with a risk of 1 ETH each. The five agents might not be aware of each other. If Alice is able to gain 5 ETH from being malicious, it would be individually rational for her to take the 2 ETH damage and gain the 5 ETH.

## Introducing trusty

trusty is a proposal for an Ethereum-wide reputation system.
It allows agents to gradually reduce their provided deposits.
Agents that are deemed trustworthy due to their past actions are allowed to (i) withdraw a relative amount of their locked and/or (ii) maintain a lower collateral threshold and would not be slashed as early as other agents.
Reputation is built over time and needs to be continuously maintained.
If a protocol deployed on Ethereum decides to integrate trusty, it reports each action of an agent back to the trusty smart contract.
In simple terms, if an action completes successfully, an agent would get a positive score.
If an action reverts due to agent error or there are disputes, the reported action would be negative.

### Continuous Actions

We record all actions of an agent within a pre-defined time period at length `t`.
Within that period, the agent can collect a score by performing desired and undesired actions as defined by the protocols integrating with trusty.
An agents motivation to behave well

### Registry of Agents

trusty keeps track of actions of agents via a registry.
An agent can have one more identities, where each public key represents an identity.
When an agent is registered with trusty at least one of its public keys is associated with a "ranking" in the registry.


