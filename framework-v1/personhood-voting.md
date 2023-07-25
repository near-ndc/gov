# NDC Personhood Voting v1

**Status: Draft**

## Abstract

We propose a powerful mechanism for human gated NDC v1 voting.
As stated in the constitution, NDC is the set of NEAR accounts representing the NEAR community (Near Digital Collective).

## Introduction

Personhood based voting requires a strong, Sybill resistant proof of personhood. There are many approaches how to achieve personhood verification:

1. Face verification: sophisticated algorithm which maps a face, assures that it is alive and computes unique ID based on the face map.
2. KYC (sumsub ...)
3. Community verification (BrightID, Proof of Humanity...)
4. Social media accounts

## Design

In Personhood based voting the voting power is equal among all NDC personhood accounts. This means that **each verified account has exactly 1 vote**.

### Personhood verification

We looked at various solutions. For v1, we want to be mindful of time and select a solid, Sybill resistant solution for human verification to release sooner than later.
After v1, our goal is to move towards multi-provider solution with stronger even stronger capabilities - the _I Am Human_ project.

We [analyzed](https://docs.google.com/document/d/111ZAJY8iqhUqo7oqF_RSaR1BX5dILtyh5E6-YkhW-tA/edit#) many solutions. Main criteria

- Sybill resistant: non human won't pass the test with a sufficiently high probability.
- Uniqueness check: same human can't generate two IDs
- Battle tested. The algorithm is heavily tested to only approve one account for the same human.
- Has sufficient market.
- Is inclusive.
- Low cost.

Throughout our analysis, we decided to use a FaceTech system. Other solutions either don't provide sufficient uniqueness guarantees (community networks, you can setup many accounts with KYC providers), require additional data collection requirements on our side (KYC providers) or are not sufficiently decentralized or battle tested.
For the Proof of Concept a [decision](https://docs.google.com/document/d/1ccPlRPvQCRsJTnoeaGYHrNYb27mjWK7aaUC4Aiw8f2U/edit?usp=sharing_eip_m&ts=63e6e810) has been drafted between GoodDollar and Verisoul and GoodDollar was selected.
NOTE: There is no NEAR native FaceTech provider (meaning that the provider issues a certificate directly on NEAR). Below we discuss an Oracle system responsible for issuing such a certificate in a form of SBT.

After PoC, in order to streamline the onboarding process, we followed the community recommendation and migrated to Fractal. Both Fractal and GoodDollar are using the same technology provider for Face Scan.

### NDC Personhood Criteria

- Account owner has been verified as unique, compared against all other verified users, using Fractal Face Scan.

### NEAR affiliation measures

Simple personhood might not be enough, if we require non trivial association with NEAR ecosystem for the NDC Governance.
We discussed additional criteria to measure association with the NEAR ecosystem, such us account activity history or stake history:

1. Have at least 1 NEAR staked.
1. Have staked at least 1 NEAR for at least 1 past month (complex requirement).
1. Have staked at least 1 NEAR for at least 1 month (very complex requirement).
1. Stakes 1 NEAR for voting (will be able to withdraw after voting finishes).
1. Proven history of NEAR activity measured by number of transactions and time.

We restrain from including them in v1 because it will significantly complexify the system (will require to implement trustless snapshot an proof verification mechanism).

### Oracle

To bridge FaceTech identity to NEAR we need an oracle. I will act as a middleware between the Fractal system and NEAR blockchain. Requirements:

- decentralized verification process
- assuring ownership of the Fractal face verified account and NEAR account.

Privacy concerns:

- Fractal doesn't provide a face metadata to assure privacy.
- We should make sure that: verifier doesn't link Fractal identities to fake or wrong accounts AND doesn't link non existing Fractal identities to NEAR accounts.

### Design and Implementation

https://github.com/near-ndc/i-am-human/blob/master/contracts/oracle/README.md

### Oracle Risks

FaceTech based solution is seen as independent solution, but it's not decentralized. In case of GoodDollar we have the following risks

- reliance on a single personhood verifier
- verifier risks: censorship, halting the system, a single point of failure.
- additional system variables
- non trivial NDC Approved Account requirements
- adding Staked NEAR as a requirement will require implementation of stake weighted voting framework.

## Consequences

Positive

- more democratic
- reduces whale impact
- using a tested, sybill resistant solution

Neutral

- good enough for start, with open, compatible path towards for next versions

Negative

- more centralized (requires a trust in the personhood proof provider)
- more complex (more variables and more moving elements)
- non trivial NDC Approved Account

## Further Notes

This is only the first step. We are planning to improve and decentralize the NEAR human protocol in the future versions. We already outlined the general ideas in `i-am-human`:

- [I Am Human early design](https://hackmd.io/ZvgUeoF4SMGM4InswH0Dsg)
- [Demystifying i-am-human](https://github.com/near-ndc/i-am-human-dapp)
- [WIP: Design](https://hackmd.io/@Kazander/ryHHniFqi)
