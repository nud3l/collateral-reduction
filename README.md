# Collateral Reduction

This repository includes code for a research project on how to reduce collateral in "passive protocols". It is an extension to the [Balance](https://eprint.iacr.org/2019/675.pdf) paper and [code](https://github.com/nud3l/layered-tcr) that should work for protocols that do not required continuous interaction by agents.

## Problem
In stablecoins, such as Dai, agents open a Collateralized Debt Position (CDP) that is over-collateralized. The over-collateralization is necessary to account for exchange rate fluctuations. However, in practice the provided collateral is much higher than the bound defined by the system. Maker provides a great [overview](https://mkr.tools/system) of the amount of collateral. Moreover, this [paper](https://arxiv.org/abs/1906.02152) by Klages-Mundt et al. shows that speculator agents de-stabalize coins.

## Objective
Honest and rational agents that act in the interest of the protocol should be able to reduce their collateral. Specifically, we want to target the speculator agents and reward them with reduced collateral for keeping the underlying coin stable.

## Approach
The start of the project will include researching the problem from a theoretical point of view and finish with a proof of concept implementation.
