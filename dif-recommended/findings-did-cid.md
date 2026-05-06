<!-- **Note:** This is a template for a "findings" document which documents
the steps that have been taken by a DID method to achieve
"DIF-recommended" status. -->

# Findings: did:cid DIF-recommended DID method

This "findings" document summarizes the process that led to the status
of `did:cid` as a DIF-recommended DID method.

This process is documented here: <https://github.com/decentralized-identity/did-methods/tree/main/dif-recommended>

**Date of this document:** 8th April 2026

## Overview

**DID method:** `did:cid`

**DID method specification:** [v1.0](https://link-to-specification)

**Open issues (3):** <https://github.com/org/didexamplemethod/issues>

**PRs (1):** <https://github.com/org/didexamplemethod/pulls>

## W3C Registry

**Yes**, see here: <https://www.w3.org/TR/did-extensions-methods/>

## Method Proposal

**Yes**, see here: <https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-example.md>

## W3C Tests

**Yes**, see here: <https://w3c.github.io/did-test-suite/#M00>

Number of tested implementations of `did:example`: **1**

### Implementation: <https://github.com/decentralized-identity/didexample-py>

**Results:** <https://github.com/w3c/did-test-suite/blob/main/packages/did-core-test-server/suites/implementations/did-example-dif-py.json>

37 passing

## Universal Resolver

**Yes**, see here:
<https://github.com/decentralized-identity/universal-resolver/blob/0000000000000000000000000000000000000000/docker-compose.yml#L000>

**Docker image:**
<https://ghcr.io/decentralized-identity/uni-resolver-driver-did-example:v1.0.0>

**Example query:**
<https://dev.uniresolver.io/#did:example:000>

## DID Traits

**Yes**, see here:
<https://identity.foundation/did-traits/#comparison-of-did-methods>

## Multiple Implementations

**Yes**, see here:
<https://link-to-information-about-implementations/>

## Deployments

**Yes**, see here:
<https://link-to-information-about-deployments/>

## Standardization Target

**Yes**, W3C

## Presentations and Deep Dives

### Initial Presentation

**Date:** Jan 01, 2025 00:00 AM

[Recording](https://link-to-recording/)

Main topics and questions by audience:

- (Drummond Reed) Asked about CREATE method. Confirmed that each DID identifier has one single registry location (e.g., Etherium vs. other blockchain), but the method supports a wide variety of registries to post CREATE and UPDATE operations. UPDATE operation allows you to migrate an identifier to another registry.
- (Jaun Caballero) How do you know you have the latest copy of the DID doc. Answer is that it is the role of your personal gatekeeper to ensure you have the latest version. This happens via a consensus methodology.
- (Grace Rachmany) How many implementations are there? How many deployments are there? Answer is they intend to have multiple implementations and deployments. See proposal for details.
- (Juan Caballero) This is similar to Sidetree. Another gossip-based method. Something to address in deep dive 1 and 2 would be how this compares to Sidetree. Concern is that gatekeepers gossip to each other and gatekeepers have to query all relevant blockchains to get latest documents. Please address failure case of what happens in a gateway is changed or if a gateway has intermittent connectivity, etc.

All questions answered and issues addressed? **Yes**

### Deep Dive 1

**Date:** Jan 01, 2025 00:00 AM

[Recording](https://link-to-recording/)

Main topics and questions by audience:

- Blockchain agnostic, update operations can specify a new network.
- Node architecture
  - Gatekeeper serves as protocol enforcer, is meant to be run by individuals themselves
  - Validates operations, stores DID events, resolves DIDs, proxies IPFS
  - Keymaster holds and signs all DID operations, seeded with a single value to allow for multiple, derived keys
  - Mediator moves operations between Gatekeeper and registries (blockchain)
  - IPFS stores content-addressed seed objects and other payloads
- (Makki Elfatih) What kind of compression is being used when pushing events to the blockchain. Answer is that transactions are not necessarily compressed, but they are batched for cost control purposes.
- (Jonathan Rayback) Pointed out Sidetree similarity. Also `did:ion`. Will cover more during second deep dive.

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
