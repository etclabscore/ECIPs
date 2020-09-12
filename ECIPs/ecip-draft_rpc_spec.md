---
eip: <to be assigned>
title: Remote procedure call specification
author: Zachary Belford <belfordz66@gmail.com>
discussions-to: https://github.com/etclabscore/ECIPs/issues/30
status: Draft
type: Standards Track
category Interface
created: 2019-09-10
replaces: 1474
---

## Simple Summary
This proposal defines a standard set of remote procedure call methods that an Ethereum node should implement.

## Abstract
Nodes created by the current generation of Ethereum clients expose inconsistent and incompatible remote procedure call (RPC) methods because no formal Ethereum RPC specification exists. This proposal standardizes such a specification to provide developers with a predictable Ethereum RPC interface regardless of underlying node implementation.

## Motivation
<!--The motivation is critical for EIPs that want to change the Ethereum protocol. It should clearly explain why the existing protocol specification is inadequate to address the problem that the EIP solves. EIP submissions without sufficient motivation may be rejected outright.-->
The motivation is critical for EIPs that want to change the Ethereum protocol. It should clearly explain why the existing protocol specification is inadequate to address the problem that the EIP solves. EIP submissions without sufficient motivation may be rejected outright.

## Specification
The specification is written in the form of an [OpenRPC](open-rpc.org) document

The specification is maintained [here](https://github.com/etclabscore/ethereum-json-rpc-specification).

The specification can be rendered as docs [here](https://playground.open-rpc.org/?uiSchema%5BappBar%5D%5Bui:splitView%5D=false&schemaUrl=https://raw.githubusercontent.com/etclabscore/ethereum-json-rpc-specification/master/openrpc.json&uiSchema%5BappBar%5D%5Bui:input%5D=false)

The specification is instrumented to produce automatic, generated clients for interacting with the JSON-RPC interface in multiple languages.

## Rationale
Much of Ethereum's effectiveness as an enterprise-grade application platform depends on its ability to provide a reliable and predictable developer experience. Nodes created by the current generation of Ethereum clients expose RPC endpoints with differing method signatures; this forces applications to work around method inconsistencies to maintain compatibility with various Ethereum RPC implementations.

Both Ethereum client developers and downstream dapp developers lack a formal Ethereum RPC specification. This proposal standardizes such a specification in a way that's versionable and modifiable through the traditional EIP process.

Previous EIP-1474 did not take into account the existance of a well defined specification for defining a service, similar to the likes of OpenAPI/Swagger or grpc. This EIP follows the some motivations, and the same methods / params. It is has simply been written into an OpenRPC, and wrapped in automated release tooling, along with other OpenRPC tools on top if you choose.

## Backwards Compatibility
This proposal impacts Ethereum client developers by requiring that any exposed RPC interface adheres to this specification. This proposal impacts dapp developers by requiring that any RPC calls currently used in applications are made according to this specification.

## Test Cases

You can test the OpenRPC document against your ethereum client in an automated fashion. See https://github.com/open-rpc/test-coverage for an example / motivation.

## Implementation

Currently most clients implement some subset / superset of these methods. The main ones being:

|Client Name|Language|Homepage|
|-|-|-|
|Geth|Go|[geth.ethereum.org](https://geth.ethereum.org)|
|Parity|Rust|[parity.io/ethereum](https://parity.io/ethereum)|
|Aleth|C++|[cpp-ethereum.org](https://cpp-ethereum.org)|

Currently, [multi-geth](https://github.com/multi-geth/multi-geth) supports both OpenRPC's `rpc.discover` method as well as the full specification.

## Copyright
Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
