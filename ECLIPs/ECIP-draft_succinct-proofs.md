---
eip: <to be assigned>
title: Succinct PoW Using Merkle Mountain Ranges
author: Zac Mitton @zmitton
discussions-to: <https://github.com/ethereum/EIPs/pulls> (Pull Number TBD)
status: Draft
type: Standards Track
category (*only required for Standard Track): Core
created: 2019-03-12
replaces (*optional): 210, 1094, 641
---

<!--You can leave these HTML comments in your merged EIP and delete the visible duplicate text guides, they will not appear and may be helpful to refer to if you edit it again. This is the suggested template for new EIPs. Note that an EIP number will be assigned by an editor. When opening a pull request to submit your EIP, please use an abbreviated title in the filename, `eip-draft_title_abbrev.md`. The title should be 44 characters or less.-->

## Simple Summary
<!--"If you can't explain it simply, you don't understand it well enough." Provide a simplified and layman-accessible explanation of the EIP.-->
The addition of a Merkle-Mountain-Range (MMR) root to blockheaders

## Abstract
<!--A short (~200 word) description of the technical issue being addressed.-->


## Motivation
<!--The motivation is critical for EIPs that want to change the Ethereum protocol. It should clearly explain why the existing protocol specification is inadequate to address the problem that the EIP solves. EIP submissions without sufficient motivation may be rejected outright.-->
The recent FlyClient [paper](https://eprint.iacr.org/2019/226.pdf) and [presentation](https://www.youtube.com/watch?v=BPNs9EVxWrA) at Scaling Bitcoin Represented a major breakthrough the ability to succinctly, and non-interactivly prove the cummulative work of a blockchain. 

Given its particularly large number of blocks (~7M+) Ethereum requires 4GB of data.
With this EIP, the same amount work going forward can already be proven in < 500kb with even a few more optimizations likely possible. This will hit a sweet spot, where for instance, mobile wallets, can request the latest cummulative work every time they are opened. Combine this with EIP-1186 (already merged), and users can finally verify data in a practical way (without a full-node).

This may also open doors for side-chains, state-channels, plasma, trustless bridges, atomic swaps, and the overall light-client-protocol.

This also solves EIPs 210, 1094, 641, (access to historic blockhashes through the EVM). A simple merkle proof can be input to prove the historic hash, with a size of ~864 bytes.


## Specification
<!--The technical specification should describe the syntax and semantics of any new feature. The specification should be detailed enough to allow competing, interoperable implementations for any of the current Ethereum platforms (go-ethereum, parity, cpp-ethereum, ethereumj, ethereumjs, and [others](https://github.com/ethereum/wiki/wiki/Clients)).-->
If `block.number >= ISTANBUL_FORK_NUM` then when constructing the block, set a 16th value `blockHashesRoot` to the header.

This Root is defined by the combining all previous hashes into a [Merkle Mountain Range](https://github.com/juinc/tilap/issues/244) (Peter Todd) using it's block number as leaf index.

Implimentaion of this tree is up to the clients but its fairly simple and requires only an additional ~500mb (on disk) to a full node.

I PoC JS implimentaion (with the real 7 million tree values) shows the following statistics:
- Calculating a `blockHashesRoot`: <X> seconds
- Creating a succinct Proof `blockHashesRoot`: <Y> seconds
- Size of a Proof <Z> mb



## Rationale
<!--The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work, e.g. how the feature is supported in other languages. The rationale may also provide evidence of consensus within the community, and should discuss important objections or concerns raised during discussion.-->


## Backwards Compatibility
<!--All EIPs that introduce backwards incompatibilities must include a section describing these incompatibilities and their severity. The EIP must explain how the author proposes to deal with these incompatibilities. EIP submissions without a sufficient backwards compatibility treatise may be rejected outright.-->
All EIPs that introduce backwards incompatibilities must include a section describing these incompatibilities and their severity. The EIP must explain how the author proposes to deal with these incompatibilities. EIP submissions without a sufficient backwards compatibility treatise may be rejected outright.

## Test Cases
<!--Test cases for an implementation are mandatory for EIPs that are affecting consensus changes. Other EIPs can choose to include links to test cases if applicable.-->
Test cases for an implementation are mandatory for EIPs that are affecting consensus changes. Other EIPs can choose to include links to test cases if applicable.

## Implementation
<!--The implementations must be completed before any EIP is given status "Final", but it need not be completed before the EIP is accepted. While there is merit to the approach of reaching consensus on the specification and rationale before writing code, the principle of "rough consensus and running code" is still useful when it comes to resolving many discussions of API details.-->
The implementations must be completed before any EIP is given status "Final", but it need not be completed before the EIP is accepted. While there is merit to the approach of reaching consensus on the specification and rationale before writing code, the principle of "rough consensus and running code" is still useful when it comes to resolving many discussions of API details.

## Copyright
Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).

