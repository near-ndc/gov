# NDC Personhood Voting v1

**Status: Draft**

## Abstract

We propose a powerful mechanism for human gated NDC v1 voting.
As stated in the constitution, NDC is the set of NEAR accounts representing the NEAR community (Near Digital Collective).

## Introduction

Personhood based voting requires a strong, Sybill resistant proof of personhood. There are many approaches how to achieve personhood verification:

1. Face verification: sophisticated algorithm which maps a face, assures that it is alive and computes unique ID based on the face map.
2. KYC:
3. Community verification (BrightID, Proof of Humanity...)
4. Social media

TODO: finish notes about other solutions

## Design

### Personhood verification

We will use battle tested, and widely used FaceTech technology. Other solutions are either centralized ()
It has a very strong accuracy as well as Sybill resistance (TODO: add research references):

- very limited or impossible to forge non-human accounts (bots don't pass the face detection algorithm).
- the algorithm is heavily tested to only approve one account for the same face. In other words, it's almost impossible to create two different FaceTech based identities by the same human.

There is no NEAR native FaceTech provider (meaning to issue a certificate directly on NEAR).

We select GoodDollar as the technology provider (TODO: link a document Noak is working on with competitive analysis).

- connections to FaceTech
- battle tested
- cheap

### Oracle

To bridge GoodDollar FaceTech identity to NEAR we need an oracle. Requirements:

- decentralized verification process
- assuring ownership of the GoodDollar face verified account and NEAR account.

We want to restrain of having one central party being an Oracle. It imposes the following risks:

- GoodDollar doesn't provide a metadata, where additional party could link metadata (eg verification data)
- Verifier being a single point of failure
- We should make sure that: verifier doesn't link GoodDollar identities to fake or wrong accounts AND doesn't link non existing GoodDollar identities to NEAR accounts.

We design a decentralized oracle. We select multiple, verified parties who will provide oracle service.
Each oracle has to provide a security stake.

Verification is done through establishing an authenticated session with GoodDollar and login with NEAR wallet.

- Authentication is established through one of the mechanisms GoodDollar provides. We check OAuth mechanism. (TODO: check if it's possible to login with face check or private key).
- User has to authenticate with all Oracles to be fully verified.
- On each positive verification, oracle adds a vote in the SBT smart contract to mint a new SBT.
- SBT is minted only when all oracles agree.

### NDC Approved Account

We need to clarify which account is approved for NDC Governance. Simple personhood might not be enough, if we require non trivial association with NEAR ecosystem.
TODO: discuss and assess ideas:

1. Have at least 1 NEAR staked.
1. Have staked at least 1 NEAR for at least 1 past month (complex requirement).
1. Have staked at least 1 NEAR for at least 1 month (very complex requirement).
1. Stakes 1 NEAR for voting (will be able to withdraw after voting finishes).
1. Proven history of NEAR activity measured by number of transactions and time (need to specify this).

### Risks

FaceTech based solution is seen as independent solution, but it's not decentralized. In case of GoodDollar we have the following risks

- relieance on a single peronhood verifier
- oracle risk: censorship, halting the system
- additional system variables
- non trivial NDC Approved Account requirements
- adding Staked NEAR as a requirement will require implementation of stake weighted voting framework.

### Consequences

Positive

- more democratic
- reduces whale impact

Neutral

Negative

- more centralized (requires a trust in the personhood proof provider)
- more complex (more variables and more moving elements)
- non trivial NDC Approved Account

## Further Notes

This is only the first step. We are planning to improve and decentralize the NEAR human protocol in the future versions. We already outlined the general ideas in `i-am-human`:

- [Demystifying i-am-human](https://github.com/near-ndc/i-am-human-dapp)
- [WIP: Design](https://hackmd.io/@Kazander/ryHHniFqi)
