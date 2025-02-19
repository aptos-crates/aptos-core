---
title: "Governance"
slug: "governance"
---
import ThemedImage from '@theme/ThemedImage';
import useBaseUrl from '@docusaurus/useBaseUrl';

# Governance

The Aptos on-chain governance is a process by which the Aptos community members can create and vote on proposals that minimize the cost of blockchain upgrades. The following describes the scope of these proposals for the Aptos on-chain governance:

- Changes to the blockchain parameters, for example, the epoch duration, and the minimum required and maximum allowed validator stake.
- Changes to the core blockchain code. 
- Upgrades to the Aptos Framework modules for fixing bugs or for adding or enhancing the Aptos blockchain functionality.
- Deploying new framework modules (at the address `0x1` - `0xa`).

## How a proposal becomes ready to be resolved

See below for a summary description of how a proposal comes to exist and when it becomes ready to be resolved:

<ThemedImage
alt="Proposal voting flow"
sources={{
    light: useBaseUrl('/img/docs/voting-resolution-flow.svg'),
    dark: useBaseUrl('/img/docs/voting-resolution-flow-dark.svg'),
  }}
/>

- The  Aptos community can suggest an Aptos Improvement Proposal (AIP) in [GitHub](https://github.com/aptos-foundation/aip).
- When appropriate, an on-chain proposal can be created for the AIP via the `AptosGovernance` module. 
- Voters can then vote on this proposal on-chain via the `AptosGovernance` module. If there is sufficient support for a proposal, then it can be resolved.
- Governance requires a minimal number of votes to be cast by an expiration threshold. However, if sufficient votes, more than 50% of th total supply, are accumulated prior to that threshold, the proposal can be executed **without waiting for the full voting period**.

## Who can propose

- To either propose or vote, you must stake but you are not required to run a validator node. However, we recommend that you be a validator with a stake and be a part of the validator set. 
- To create a proposal, the proposer's backing stake pool must have the minimum required proposer stake. The proposer's stake must be locked up for at least as long as the proposal's voting period. This is to avoid potential spammy proposals. 
- Proposers can create a proposal by calling [`AptosGovernance::create_proposal`](https://github.com/aptos-labs/aptos-core/blob/27a255ebc662817944435349afc4ec33ea317e64/aptos-move/framework/aptos-framework/sources/aptos_governance.move#L183).

## Who can vote

- To vote, you must stake, though you are not required to run a validator node. Your voting power is derived from the backing stake pool. 
- Voting power is calculated based on the current epoch's active stake of the proposer or voter's backing stake pool. In addition, the stake pool's lockup must be at least as long as the proposal's duration.

:::tip
Each stake pool can only be used to vote on each proposal exactly once.
:::
