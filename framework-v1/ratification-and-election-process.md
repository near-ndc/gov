# Ratification and Election Process

**Status: Draft**

We still need to decide about the voting mechanism: [Stake Weighted Voting](./stake-weighted-voting.md) (**SWV**) or [Personhood Voting](./personhood-voting.md) (**PV**).
This document in few places assumes SWV (especially the roadmap, which needs to be updated).

## Synopsis

For v1 governance, there is a need to ratify the Constitution and elect the houses. Our goal is to empower NEAR community for that process rather than having it centrally appointed by a few entities (as that would be against the ethos of the NDC).

Today we don’t have a good way to measure the community voice that is available and not gameable. Eventually, our preference is quadratic voting by human-verified accounts. Until then, we propose v1 NDC voting as described below. That includes:

- [Constitution](https://github.com/near-ndc/constitution) Ratification
- Community Treasury Ratification
- Community Treasury directive to issue funds (if not directed by House of Merit) 
- Election for House of Merit (15 seats) and Council of Advisors (7 seats) and Transparency Commission
- Veto 

## Roadmap

1. NDC to provide guidelines for running a candidacy:
   1. Timeline;
   1. Template document, how a candidate can propose himself.
      Sections: Summary (2 sentences introducing a profile), Motivation Letter, Profile (what the candidate wants to focus on, what is his vision), Resume (achievements, contributions).
   1. Profiles should be described in gov forum – this way users can easily contribute and ask questions.
   1. Guidelines how and where to make polls (let’s focus on 3 solutions max, proposal: NEARSocial, gov forum, telegram).
1. NDC to provide a support team:
   1. Help with communications.
   1. Help to schedule AMMs.
1. NDC & Proximity to provide required smart contract, services and UI for running the voting and elections.
1. NDC to setup a telegram notifications channel. The NDC communication team will provide updates about:
   1. New candidates and copy pasting the summary line;
   1. Scheduled AMMs.
1. Proximity to create Stake Weighted Oracle and proof services (proof generation UI & backend, proof verification smart contract & UI).
1. NDC to create voting contracts: a) constitution ratification and b) elections.
1. Organize 2 workshops about the process (internal and external).
1. Contract demos.

![v1 timeline](assets/v1-timeline.png)

## Voting

_Voting Body_ is the NEAR Ecosystem general assembly for elections, referendums, and voting comprised of every NEAR Account (account) designated as a voting account.

Voting is happening on chain. For v1, the Voting Body is set of accounts staking NEAR (delegated to validators), except staking pools and other identified smart contracts and entities who are known to aggregate stake.

The voting mechanism is either [Stake Weighted Voting](./stake-weighted-voting.md) (**SWV**) or [Personhood Voting](./proof-of-personhood-voting.md) (**PPV**) (active discussion).

Each proposal will have `start_time` and `end_time`. Vote cast can only happen between `start_time` and `end_time` (inclusively).

Below we define requirements for three different scenarios. 

For Stake-Weighted voting:

- **NEAR Quorum Requirement** means, in respect of a vote, that votes are cast by the holders of at least `5%` of all Staked NEAR on the NEAR Blockchain.
- **NEAR Big Quorum Requirement** means, in respect of a vote, that votes are cast by the holders of at least `8%` of all Staked NEAR on the NEAR Blockchain.
- **NEAR Supermajority Consent** means the approval of a proposal (including a Community Proposal), matter and/or decision by the NEAR Community, where a vote of the NEAR Community in relation to that proposal (including a Community Proposal), matter and/or decision takes place and the following apply in respect of that vote:
   - 1 Staked NEAR = 1 vote;
   - the NEAR Big Quorum Requirement is met;
   - `#yes_votes >= 60% × (#yes+#no_votes)` of all cast votes (#yes+#no+#abstain_votes)
- **NEAR Consent** -- similar to Supermajority Consent:
   - 1 Staked NEAR = 1 vote;
   - the NEAR Quorum Requirement is met
   - `#yes_votes > #no_votes` of all cast votes (#yes+#no+#abstain_votes)

For Proof-of-Personhood Voting:

- **NDC Approved Account**: verified personhood accounts using a combination of all of the following criteria
   -  Account owner has passed KYC and been verified as 16 years or older (for clarity: no need for any other KYC datapoints)  
   -  Account owner has been verified as unique by using a Face Verification software, compared agains all other verified users [GoodDollar | Verisoul (waiting for final decision)]
   -  Account has staked 1 NEAR or more
   -  [TODO: need to double check if we want to add additional requirement about the account history or stake, but that will again complexify the system and will require blockchain snapshot + proof verifier]
- **NEAR Quorum Requirement** means, in respect of a vote, that votes are cast by at least [ 2000 ] NDC Approved Accounts
- **NEAR Big Quorum Requirement** means, in respect of a vote, that votes are cast by at least [ 4000 ] NDC Approved Accounts
- **NEAR Supermajority Consent** and means the approval of a proposal (including a Community Proposal), matter and/or decision by the NEAR Community, where a vote of the NEAR Community in relation to that proposal (including a Community Proposal), matter and/or decision takes place and both of the following apply in respect of that vote:
   - 1 NDC Approved Account = 1 vote;
   - the NEAR Big Quorum Requirement is met;
   - `#yes_votes >= 60% × (#yes+#no_votes)` of all cast votes (#yes+#no+#abstain_votes)
- **NEAR Consent** -- similar to Supermajority Consent:
   - 1 NDC Approved Account = 1 vote;
   - the NEAR Quorum Requirement is met
   - `#yes_votes > #no_votes` of all cast votes (#yes+#no+#abstain_votes)

For Personhood Voting with Stake Weight Quorum:

- **NDC Approved Account**: has the same meaning as for _Proof-of-Personhood Voting_ above.
- **NEAR Quorum Power** is the sum of cubic root of the staked NEAR of each voting NDC approved account that had staked at the time pointed the proposal (resolved as a snapshot). The each voting account

        struct Proposal {
            // ...
            stakeTree: StakeSnapshot
        }

        quorum_power(p: Proposal, voters: []AccuntId) -> u128 {
            voters
                .map(|a| -> pow(p.stakeTree.accountStake(a)), 1/3) // TODO: need to make it deterministic
                .sum()
        }

- **NEAR Quorum Requirement** means, in respect of a vote, that the Quorum Power must be greater than the Quorum Threshold which is defined as the cubic root of (5% of all staked NEAR) plus 2000.
- **NEAR Big Quorum Requirement** means, in respect of a vote, that the Quorum Power must be greater than the Quorum Threshold which is defined as the cubic root of (8% of all staked NEAR) plus 2000.
- **NEAR Supermajority Consent** and **NEAR Consent** have the same meaning as in _Proof-of-Personhood Voting_ above

### Constitution

Constitution Proposal will provide 3 options: `yes`, `no` and `abstain`. The reason we are including abstain is to make the quorum more meaningful: people who don’t want to take a side (yes / no) but want to be counted into the quorum can do so. For example, if the NEAR Foundation doesn’t want to vote yes/no, but want to support the initiative, then NF can vote abstain.

Each account can vote multiple times withing the proposal voting period. Each subsequent vote will overwrite the previous one.
When casting a vote, an account allocates credits equal to his/her voting power to the selected option.

Examples above assume SWV for quorum.

Example: if a voter has 10stake and cast vote by selecting _yes_, the smart contract `#yes` counter will increase by 10 and will add the voters' account to the set of account who already voted.
The proposal passes when **NEAR Supermajority Consent** is met:

    quorum:    #yes + #no + #abstain >= 0.08 x total_staked_near
    threshold: #yes > 0.6 x (#yes + #no)

Example of a proposal passing (assuming there are 500 stake in total):

    yes=65stake, no=35stake, abstain=10
    yes=8stake, no=2stake, abstain=50

Example of a proposal NOT passing (assuming there are 500 stake in total):

    yes=60stake, no=40stake, abstain=any   – didn’t pass the threshold
    yes=8stake, no=2stake, abstain=20   – not enough quorum

### House of Merit and Council of Advisors

TODO: this

There will be 2 proposals in a StakeWeight Ranking smart contract: one for House of Merit and the second one for Council of Advisors. Each proposal will be filled with a list of candidates who are running for elections.

Each account from the _Voting Body_ will be able to cast 1 vote and support maximum 10 candidates by dividing his/her stake credits between the candidates. Contract tally will happen in real time: candidates will be sorted by rank in the smart contract. In the House of Merits proposal, top `15` candidates will be selected as the members of the house. Similarly, top `7` will be selected for Council of Advisors.

Example: we have 50 candidates: `c1, c2, ..., c50`.

- Voter1 has 100stake and will cast his vote by providing whole support for candidate `c10`: after that, `c1` score will increase by 100.
- Voter2 has 200stake and will cast his vote by providing 50stake support for candidate `c1`, 20stake support for candidate `c20` and 140stake support for candidate `c21`. After that, `c1` score will increase by 50, `c20` score will increase by 20 and `c21` score will increase by 140.

### Other voting proposals

The NDC will be able to vote on other proposals such us:

- Approve The Term Budget for Congress - NEAR Quorum Requirement
- Approve Protocol Changes - NEAR Quorum Requirement
  TODO: maybe we will push this to v2 to reduce complexity in v1.

## Transparency Commission

TODO: provide process of electing the Transparency Commission
7 seats
