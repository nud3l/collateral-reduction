# Secure Collateral Reduction for Many Protocols

In decentralized ledgers, deposits replace implicit trust. Instead of an explicit ranking (e.g. stars on Amazon or karma on Reddit) or personal relationships, an agent (human or machine) trusts another agent (human or machine) if enough coins are provided. These coins represent an assurance that the counterparty has skin in the game. The idea is that if the counterparty misbehaves, a mechanism is able to punish the cheating party and reimburse the agent suffering from those actions.

So everything solved in blockchain paradise? Not quite. Determining how much deposit an agent is required is a tricky question. The more deposit an agent has to provide the more "safety" a protocol has as it increases the potential punishment in case of misbehaviour. However, the more deposit required the smaller the set of agents that have enough coins to qualify for participation.

Even worse, most protocols need to account for two main sources of uncertainty. (1) The relative value of the deposit in relation to the risk might change over time, i.e. it is event-dependent. For example, in Dai 150% collateral is required to account for sudden price shocks of the underlying Ether to USD price. (2) Private information needs to be accounted for. For example, an agent might have some hidden motivations, external incentives (bribing), or simple can choose between different protocols.

Event-dependency and private information usually require protocols to over-collateralize. Simply put, if the risk is of value `1`, you add an over-collateralization factor `f` that accounts for both sources of uncertainty. This is the case for most DeFi protocols like Dai or Compound. In other protocols, say TrueBit or PoS staking the risk is not entirely clear. So you have to estimate the risk and require some form of deposit.

## trusty

We proposed trusty as a remedy to the problem of over-collateralization. We do not solve the problem of determining how much collateral is required, but rather offer a way to *securely* reduce existing collateral requirements to a lower bound. trusty is intended to be a plug-in to a range of different protocols.

Suitable protocols for our mechanism have the following properties:

- Require deposits to protect against rational adversaries.
- Require over-collateralization (or have no clearly assigned risk value).
- Require eventually finalized decisions whether or not an agent behaved correctly.

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


