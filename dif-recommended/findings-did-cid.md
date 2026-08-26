# Findings: did:cid DIF-recommended DID method

This "findings" document summarizes the process that led to the status
of `did:cid` as a DIF-recommended DID method.

This process is documented here: <https://github.com/decentralized-identity/did-methods/tree/main/dif-recommended>

**Date of this document:** 3rd August 2026

## Overview

**DID method:** `did:cid`

**DID method specification:** [Specification](https://archon.technology/specs) ([source](https://github.com/archetech/archon/blob/main/docs/scheme.md); Archon [v0.11.0](https://github.com/archetech/archon/releases/tag/v0.11.0))

**Open issues (36):** <https://github.com/archetech/archon/issues>

**PRs (18):** <https://github.com/archetech/archon/pulls>

## W3C Registry

**Yes**, see here: <https://www.w3.org/TR/did-extensions-methods/> (<https://github.com/w3c/did-extensions/blob/main/methods/cid.json>)

## Method Proposal

**Yes**, see here: <https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-cid.md>

## W3C Tests

**Yes**, see here: <https://w3c.github.io/did-test-suite/> (fixture added in <https://github.com/w3c/did-test-suite/pull/240>)

Number of tested implementations of `did:cid`: **1**

### Implementation: <https://github.com/archetech/archon>

**Results:** <https://github.com/w3c/did-test-suite/blob/main/packages/did-core-test-server/suites/implementations/did-cid.json>

Published suite report includes Archon `did:cid` results (e.g. 58 / 3 identifier-related counts; 38 production for DID v1.0 and DID v1.1).

## Universal Resolver

**Pending** — driver proposed in <https://github.com/decentralized-identity/universal-resolver/pull/573>.

Driver source: <https://github.com/archetech/uni-resolver-driver-did-cid>

**Docker image:**
<https://ghcr.io/archetech/uni-resolver-driver-did-cid:0.1.0>

**Example query (Archon-hosted resolver):**
<https://resolver.archon.technology/1.0/identifiers/did:cid:bagaaieraxdxq4fm2kjh6yqjxjor3t2idczkmxd4v7in4u353fa6m6sms2pnq>

## DID Traits

**Pending** — traits submission proposed in <https://github.com/decentralized-identity/did-traits/pull/70>.

Comparison table (once merged):
<https://identity.foundation/did-traits/#comparison-of-did-methods>

The method proposal notes support for Decentralized, Persistent, Cryptographically Verifiable, and Resolvable traits.

## Multiple Implementations

**Yes**, see here:
<https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-cid.md>

- TypeScript / Node.js reference implementation (`@didcid/gatekeeper`, `@didcid/keymaster`, `@didcid/cipher`) in <https://github.com/archetech/archon>
- Native Python Keymaster: <https://github.com/archetech/archon/pull/455>
- Native Rust Gatekeeper: <https://github.com/archetech/archon/pull/404>

## Deployments

**Yes**, see here:
<https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-cid.md>

Production infrastructure includes Gatekeeper API, DID explorer, web wallet, naming service, and independently operated nodes (e.g. archon.technology, 4tress.org).

## Standardization Target

**No**, further standardization not currently sought

## Presentations and Deep Dives

### Initial Presentation

**Date:** Apr 8, 2026

[Recording](https://us02web.zoom.us/rec/share/qh6ihv-jW1RlJQ2eGT-1ysJE4dpswngJ65BogDwub5K3g29m74ncuIegXFsOukgI.pyISp0q_iHUSii8k)

Main topics and questions by audience:

- (Drummond Reed) Asked about CREATE method. Confirmed that each DID identifier has one single registry location (e.g., Etherium vs. other blockchain), but the method supports a wide variety of registries to post CREATE and UPDATE operations. UPDATE operation allows you to migrate an identifier to another registry.
- (Jaun Caballero) How do you know you have the latest copy of the DID doc. Answer is that it is the role of your personal gatekeeper to ensure you have the latest version. This happens via a consensus methodology.
- (Grace Rachmany) How many implementations are there? How many deployments are there? Answer is they intend to have multiple implementations and deployments. See proposal for details.
- (Juan Caballero) This is similar to Sidetree. Another gossip-based method. Something to address in deep dive 1 and 2 would be how this compares to Sidetree. Concern is that gatekeepers gossip to each other and gatekeepers have to query all relevant blockchains to get latest documents. Please address failure case of what happens in a gateway is changed or if a gateway has intermittent connectivity, etc.

All questions answered and issues addressed? **Yes**

### Deep Dive 1

**Date:** May 6, 2026

[Recording](https://us02web.zoom.us/rec/share/RTa6XRppMds3qvx9juugTRQHRzM2oVrtXwRZOoQEYUDZjeXPyz0HinkuOULeVSCH.r36x4ne12WUxYakv)

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

**Date:** May 27, 2026

[Recording](https://us02web.zoom.us/rec/share/RHeE9hypV_3MLi4zxaQs8wZ6VJt2sA-15xnf8JMESVho5gNFCI-WMJh7CDqGIrsZ.6lMQN_gtrkBWyokf)

Main topics and questions by audience:

- Comparison with Sidetree
  - Gatekeeper composes DID Document based on executing the correct series of operations, Sidetree does not.
  - Sidetree has recovery capabilities such as a recovery key that `did:cid` does not. Recovery occurs at application layer rather than at protocol level.
  - See [detailed comparison table](https://github.com/archetech/archon/blob/main/docs/sidetree-archon-comparison.md)
- (Juan Caballero) How do Gatekeepers know where to get all necessary info from?
  - You can assign helper nodes to fill in missing info for you.
- (Otto Mora) Is all credential storage local?
  - Archon is very composable - there are a number of different ways to distribute the pieces.
  - Different capabilities can be programmed at the service or application layer.
- (Juan Cabellero) Are there multiple implementations?
  - There are several implementations that the Archon implementers have done. No external implementations yet.
  - Gatekeeper has implementations in typescript and  rust. Keymaster has implementations in typescript and python.
- (Juan Cabellero) What happens if blockchain substrate state is ambiguous?
  - Gatekeeper will mark ambiguous information as "not confirmed" until it can disambiguate. Wait for confirmation block if high risk is involved.
  - Mediators handle chain reorgs deterministically.

All questions answered and issues addressed? **Yes**

## Pull Request for DIF-recommended status

<https://github.com/decentralized-identity/did-methods/pull/103> **(15 comments)**

Main questions and topics:

- (jrayback) Opened the 60-day formal review period (ending 26 Jul 2026)
- (ottomorac) Requested W3C DID Methods Registry listing and W3C DID test-suite coverage before approval
- (Flaxscrip) Add Privacy and Security considerations per DID Core; later reported DID-Core-conformant published specs at <https://archon.technology/specs>
- (jrayback) Register any non-core DID document properties; (Flaxscrip) no additional property registration needed after Core alignment
- (Flaxscrip) Confirmed W3C registry entry; published Universal Resolver driver image; opened Universal Resolver driver PR <https://github.com/decentralized-identity/universal-resolver/pull/573>
- (ottomorac / macterra) W3C test-suite PR <https://github.com/w3c/did-test-suite/pull/240> progressed from draft to review and was merged
- (gobengo) Asked whether the method is compatible with [“DIF is for humans”](https://blog.identity.foundation/dif-is-for-humans/); (GraceRachmany) clarified that DIF AI policy applies to DIF-owned repositories, `did:cid` is not a DIF-donated work item, and the WG can review the request on its merits; (Flaxscrip) confirmed human authorship of contributions

All questions answered and issues addressed? **Yes**
