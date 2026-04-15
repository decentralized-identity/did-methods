# Findings: did:example DIF-recommended DID method

This "findings" document summarizes the process that led to the status
of `did:example` as a DIF-recommended DID method.

This process is documented here: <https://github.com/decentralized-identity/did-methods/tree/main/dif-recommended>

**Date of this document:** 15th April 2026

## Overview

**DID method:** `did:ethr`

**DID method specification:** [v1.0](https://github.com/decentralized-identity/ethr-did-resolver/blob/master/doc/did-method-spec.md)

**Open issues (3):** <https://github.com/decentralized-identity/ethr-did-resolver/issues>

**PRs (0):** <https://github.com/decentralized-identity/ethr-did-resolver/pulls>

## W3C Registry

**Yes**, see here: <https://www.w3.org/TR/did-extensions-methods/>

## Method Proposal

**Yes**, see here: <https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-ethr.md>

## W3C Tests

**Yes**, see here: <https://w3c.github.io/did-test-suite/#M14>

Number of tested implementations of `did:ethr`: **TBD**

### Implementation: <https://github.com/decentralized-identity/ethr-did-resolver/>

**Results:** <https://github.com/w3c/did-test-suite/blob/main/packages/did-core-test-server/suites/implementations/dereferencer-ethr-2021-consensys-mesh.json>

2 passing

## Universal Resolver

**Yes, incorporated into uniresolver directly**, see here:
<https://github.com/decentralized-identity/universal-resolver/blob/1410aff24131f2e0fbc5151a5954a452b45b170d/uni-resolver-web/src/main/resources/application.yml#L73-L80>

**Docker image:**
n/a

**Example query:**
<https://dev.uniresolver.io/#did:ethr:mainnet:0x3b0bc51ab9de1e5b7b6e34e5b960285805c41736>

## DID Traits

**NOT YET**, see here:
<https://github.com/decentralized-identity/did-traits/tree/main/methods>

## Multiple Implementations

**TBD**, see here:
<https://link-to-information-about-implementations/>

## Deployments

**TBD**, see here:
<https://link-to-information-about-deployments/>

## Standardization Target

**TBD**

## Presentations and Deep Dives

### Initial Presentation

**Date:** Apr 1, 2026 17:00 UTC

[Recording](https://us02web.zoom.us/rec/share/AphrjaZ6ha9zv6Z4sMsc1du9WG6BcyFkq8uCGry-xiruG-o58ggjuvSlNsjD4HFQ.Hq5JIy4LthJL1t4z)

Main topics and questions by audience:

- Drummond: Is this a SCID? Mircea: Yes, initial is SCID, blockchain is witness to verifiable history
- (Participant 2) Topic 2

All questions answered and issues addressed? **Yes**

### Deep Dive 1

**Date:** Apr 15, 2026 17:00 UTC

[Recording](https://link-to-recording/)

Main topics and questions by audience:

- Tour of [proposal PR](https://github.com/decentralized-identity/ethr-did-resolver/blob/master/doc/did-method-spec.md)
  - sidebar: DID update can rotate control to a smart contract w/arbitrary superpowers (multisig, other keys with precompile, ZK, etc)
  - sidebar: implicit use makes usage metrics impossible; in uPort days a tiny percentage every updated/rotated off of implicit DID
  - sidebar: energy consumption (trivial, other than the eth nodes themselves)
  - sidebar: crypto agility: various key types inherent to EVM, including recently added P-256, some additional one available on specific chains (e.g. ZK L2s); 
    - did DOCUMENT ITSELF can express any key that fits in a JSON string, even if can't be verified onchain
- Christian: Better explanation of how ERCs/EIPs define smart contracts?
  - BF: Solidity and ABIs in 90seconds
  - Mircea: no, ERC defines (and was accompanied by) reference implementation but people make variants w/ additional functions on private networks; permissionless; see Energy Web example linked from proposal PR
- Slides
  - core CRUD mechanics
    - only keys and serviceEndpoints; these are NOT profiles, don't add user-generated content! blockchains are append-only!
  - registry
  - live onchain demo + uniresolver !!!
  - Sidebar on multisig
    - Jonathan: but multisig rules/logic not encoded in the did doc, right? Mircea: no, EVM just makes any signer (offchain or on-) an opaque address; you have to look up that logic somewhere else (etherscan for known/public contracts for ex.)
    - Also arbitrary keys can be added to any DID Doc if it has a registered LD-suite; even CProof2022 !!!

All questions answered and issues addressed? **Yes**

### Deep Dive 2

**Date:** Jan 01, 2025 00:00 AM

[Recording](https://link-to-recording/)

Main topics and questions by audience:

- (Participant 1) Topic 1
- (Participant 2) Topic 2

All questions answered and issues addressed? **Yes**

## Pull Request for DIF-recommended status

<https://github.com/decentralized-identity/did-methods/pull/00> **(3 comments)**

Main questions and topics:

- (Participant 1) Topic 1
- (Participant 2) Topic 2

All questions answered and issues addressed? **Yes**
