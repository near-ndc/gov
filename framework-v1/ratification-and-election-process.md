# Ratification and Election Process

**Status: Draft**

For Proof of Concept we decided to use [Personhood Voting](./personhood-voting.md) (**PV**).
Our early design included [Stake Weighted Voting](./stake-weighted-voting.md) (**SWV**).

## Synopsis

Our goal is to empower NEAR community for that process rather than having it centrally appointed by a few entities (as that would be against the ethos of the NDC). We are designing a secure, non gameable way to measure the community voice that is available.

For v1 governance, there is a need to elect the houses. The legal WG decided to not do official Constitution ratification and voting, and instead to use it as a guideline, vision.

In v1, our principle is **1 human 1 vote**. Eventually, we may move to other mechanism, like quadratic voting by human-verified accounts. Until then, we propose v1 NDC voting as described below.

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

## Voting

_Voting Body_ is the NEAR Ecosystem general assembly for elections, referendums, and voting comprised of every NEAR Account (account) designated as a voting account.
Voting happens on chain. The voting mechanism and the v1 Voting Body is defined in [Personhood Voting](./personhood-voting.md) (**PV**) (active discussion).
Each proposal will have `start_time` and `end_time`. Vote cast can only happen between `start_time` and `end_time` (inclusively).

Below we define requirements for three different scenarios.

#### Proof-of-Personhood Voting Thresholds

- **NDC Approved Account**: a proof of personhood verified account.
- **NEAR Quorum Requirement** means, in respect of a vote, that votes are cast by at least [ 1000 ] NDC Approved Accounts
- **NEAR Big Quorum Requirement** means, in respect of a vote, that votes are cast by at least [ 2000 ] NDC Approved Accounts
- **NEAR Consent** means the approval of a proposal (including a Community Proposal), matter and/or decision by the NDC, where a vote of the NDC in relation to that proposal (including a Community Proposal), matter and/or decision takes place and both of the following apply in respect of that vote:
  - the NEAR Quorum Requirement is met;
  - the number of "yes" votes cast is more than 50% of the sum of "yes" and "no" votes: `#yes_votes > #no_votes` (we don't consider abstain votes for the threshold).
- **NEAR Supermajority Consent** -- similar to Supermajority Consent:
  - the NEAR Big Quorum Requirement is met;
  - the number of "yes" votes cast is more than 60% of the sum of "yes" and "no" votes: `#yes_votes > 60% × (#yes_votes + #no_votes)` (we don't consider abstain votes for the threshold).

### Constitution

Constitution Proposal will provide 3 options: `yes`, `no` and `abstain`. The reason we are including abstain is to make the quorum more meaningful: people who don’t want to take a side (yes / no) but want to be counted into the quorum can do so. For example, if the NEAR Foundation doesn’t want to vote yes/no, but want to support the initiative, then NF can vote abstain.

Each account can vote multiple times withing the proposal voting period. Each subsequent vote will overwrite the previous one.
When casting a vote, an account allocates credits equal to his/her voting power to the selected option.

#### Examples with PV

A voter passed a personhood verification and cast vote by selecting _yes_, the smart contract `#yes` counter will increase by 1 and will add the voters' account to the set of account who already voted, prohibiting him casting another vote.
The proposal passes when **NEAR Supermajority Consent** is met:

    quorum:    #yes + #no + #abstain >= 2000
    threshold: #yes > 0.6 x (#yes + #no)

Examples of a proposal passing (assuming 500 personhood verified accounts voted):

    yes=65accounts, no=35accounts, abstain=10accounts
    yes=8accounts, no=2accounts, abstain=50accounts

Example of a proposal NOT passing (assuming 500 personhood verified accounts voted):

    yes=260accounts, no=240accounts, abstain=0        – didn’t pass the threshold
    yes=60accounts, no=40accounts, abstain=any        – didn’t pass the threshold
    yes=8accounts, no=2accounts, abstain=20accounts   – not enough quorum

### House of Merit and Council of Advisors

There will be 2 proposals in a Ranking smart contract: one for House of Merit and the second one for Council of Advisors. Each proposal will be filled with a list of candidates who are running for elections.

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
