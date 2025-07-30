# DIF-recommended DID Methods

This page describes a process for DID methods to achieve a status of "DIF-recommended DID Method", which is intended to be a label for DID methods that comply with DIF's published evaluation criteria and have passed the review process.

The process is as follows:

1. The method advocate submits the DID method for consideration following [the documented procedure](https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/README.md).
1. The advocate presents the proposal template contents during a working group meeting and receives initial feedback.
1. When the method meets the criteria outlined in the table below, the advocate schedules the first deep dive with the working group chairs during a regular meeting.
1. The first deep dive occurs, where the group provides detailed feedback on the method's maturity and compliance with requirements.
1. The advocate addresses any concerns raised before scheduling the second deep dive with the chairs. The second deep dive must occur at least two weeks after the first.
1. The second deep dive takes place. Duration varies based on remaining concerns and new issues raised.
1. After the second deep dive, the working group chairs submit a PR changing the table's last column from 'no' to 'yes', signaling the start of the formal review period.
1. The 60-day formal review period begins immediately after the second deep dive and is announced publicly via relevant DIF mailing lists.
1. During the formal review period, all questions or concerns must be addressed through PR comments. Active discussion is expected for each method.
1. If no outstanding questions, concerns, or objections remain at the end of the formal review period, the chairs merge the PR and the method attains DIF Recommended Status.

The following table tracks DID methods that are currently participating in this process.

| Method | Spec Version | W3C Registry | Proposal | W3C Tests | Universal Resolver | DID Traits | Multiple Impls | Deployment | Standards Target | Two Deep Dives | DIF Recommended |
|--------|--------------|--------------|----------|-----------|-------------------|------------|----------------|------------|------------------|------------|-----------------|
| `did:cheqd` | [ADR Stage ACCEPTED](https://docs.cheqd.io/product/architecture/adr-list/adr-001-cheqd-did-method) | Yes | [Yes](https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-cheqd.md) | [Yes](https://github.com/w3c/did-test-suite/blob/main/packages/did-core-test-server/suites/implementations/resolver-did-cheqd.json) | Yes | Yes | ? | ? | ? | 0 | **No** |
| `did:ebsi` | [Last updated on Mar 3, 2025](https://hub.ebsi.eu/vc-framework/did/legal-entities) | No | No | [Yes](https://github.com/w3c/did-test-suite/blob/main/packages/did-core-test-server/suites/implementations/did-ebsi.json) | Yes | No | ? | ? | European Standard at CEN/CLC JTC 19 WG 1 | 0 | **No** |
| `did:iden3` | [Specification](https://github.com/iden3/did-iden3/blob/main/did-iden3-method.md) | Yes | [Yes](https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-iden3.md) | No | Yes | Yes | ? | ? | European Standard at CEN/CLC JTC 19 WG 1 (planned) | 0 | **No** |
| `did:key` | [Draft Community Report v0.7](https://w3c-ccg.github.io/did-key-spec/) | Yes | [Yes](https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-key.md) | [Yes](https://github.com/w3c/did-test-suite/blob/main/packages/did-core-test-server/suites/implementations/did-key-2020-db.json) | Yes | Yes | ? | ? | W3C Recommendation at W3C DID Methods WG | [1](https://github.com/decentralized-identity/did-methods/blob/main/AGENDA.md#meeting---26-mar-2025---1800-cet) | **No** |
| `did:peer` | [v1.0 Draft](https://identity.foundation/peer-did-method-spec/) | Yes | Yes | No | Yes | Yes | ? | ? | DIF-Approved Deliverable at DIF ID WG | [1](https://github.com/decentralized-identity/did-methods/blob/main/AGENDA.md#meeting---23-apr-2025---1800-cest) | **No** |
| `did:scid` | [Working Draft 03](https://lf-toip.atlassian.net/wiki/spaces/HOME/pages/88572360/DID+SCID+Method+Specification) | Yes | [Yes](https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-scid.md) | No | Yes | No | ? | ? | ToIP-Approved at ToIP DID SCID Task Force | 0 | **No** |
| `did:web` | [Unofficial Draft](https://w3c-ccg.github.io/did-method-web/) | Yes | [Yes](https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-web.md) | [Yes](https://github.com/w3c/did-test-suite/blob/main/packages/did-core-test-server/suites/implementations/did-web-spruce.json) | Yes | Yes | ? | ? | W3C Recommendation at W3C DID Methods WG | 0 | **No** |
| `did:webplus` | [Specification](https://ledgerdomain.github.io/did-webplus-spec/) | No | [Yes](https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-webplus.md) | No | No | No | ? | ? | ? | 0 | **No** |
| `did:webs` | [Implementors Draft v0.9.15](https://trustoverip.github.io/tswg-did-method-webs-specification/) | No | [Yes](https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-webs.md) | No | Yes | No | ? | ? | ? | 0 | **No** |
| `did:webvh` | [Current Stable v1.0](https://identity.foundation/didwebvh/v1.0/) | Yes | [Yes](https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-webvh.md) | [Yes](https://w3c.github.io/did-test-suite/#M51) | Yes  | [Yes](https://identity.foundation/did-traits/#comparison-of-did-methods) | [5](https://didwebvh.info/latest/implementations/)   | [Yes](https://didwebvh.info/latest/implementations/deployments/) | W3C | [Intro](https://us02web.zoom.us/rec/share/AJ5AINNqN0mc-gDtSsKPjgyknBjXViRsVpXklZFcC4vObcrRxAoXQ3c9kCRkmEKA.ZAK46kp3nq77dWIm), [Deep Dive 1](https://us02web.zoom.us/rec/share/6GhsVQ6VCIQiM5YyqkeAr4zg9RxcfxriKSi3tqQp5v0nad7Gdp52uXe5Pm3B26nz.SdHHNRMZJJcWmzZn), [Deep Dive 2](https://us02web.zoom.us/rec/share/lfV6HHLI9JrbIihvji3aChwKMzpKNuAYstXwHjcAAXbBI6pt1e1GTGheEY-vR0G6.xRejirZnUaAxQB3_) | **No** |

## Column Definitions

1. **Method**: DID Method Name (alphabetical order)
1. **Spec Version**: DID Method Spec Version (must be some kind of final version, include link to specification)
1. **W3C Registry**: Registered in W3C Methods Registry (see <https://www.w3.org/TR/did-extensions-methods/>)
1. **Proposal**: Method Proposal Template (include link to proposal file at <https://github.com/decentralized-identity/did-methods/tree/main/method-proposals>)
1. **W3C Tests**: Passed W3C Test suite (include link to W3C test suite data at <https://github.com/w3c/did-test-suite/tree/main/packages/did-core-test-server/suites/implementations>)
1. **Universal Resolver**: Supported in DIF Universal Resolver (see <https://github.com/decentralized-identity/universal-resolver>)
1. **DID Traits**: Evaluation in DID Traits (see <https://identity.foundation/did-traits/>). A DID Method does not need to exhibit every DID trait to be considered for recommended status.
1. **Multiple Impls**: Multiple implementations (include proof of multiple implementations, could be in the proposal file at column 4)
1. **Deployment**: Significant Deployment (include proof of significant deployment, could be in the proposal file at column 4). This is, by definition, a subjective measurement. Please provide as much detailed context as possible.
1. **Standards Target**: Standardization Target (include link to ongoing standardization process, or link to final document once the standardization target has been reached). This is optional.
1. **Two Deep Dives**: Conducted two Deep Dives (include link to meeting recording/notes, e.g., at <https://github.com/decentralized-identity/did-methods/blob/main/AGENDA.md>)
1. **DIF Recommended**: DIF-recommended DID Method (DID method becomes "DIF-recommended" after DIF Technical Steering Committee confirms that all requirements have been met)
