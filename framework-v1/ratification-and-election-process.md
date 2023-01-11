# Ratification and Election Process

The document describes how the process and timeline and process for the NDC v1 ratification. That includes:

- [Constitution](https://github.com/near-ndc/constitution) Ratification
- Election for House of Merit and Council of Advisors

TODO: provide parameters for houses

## Overview

1. NDC to provide guidelines for running a candidacy:
   1. Timeline;
   1. Template document, how a candidate can propose himself.
      Sections: Summary (2 sentences introducing a profile), Motivation Letter, Profile (what the candidate wants to focus on, what is his vision), Resume (achievements, contributions).
   1. Profiles should be described in gov forum – this way users can easily contribute and ask questions.
   1. Guidelines how and where to make polls (let’s focus on 3 solutions max, proposal: NEARSocial, gov forum, telegram).
1. NDC to provide a support team:
   1. Help with communications.
   1. Help to schedule AMMs.
1. NDC to setup a telegram notifications channel. The NDC communication team will provide updates about:
   1. New candidates and copy pasting the summary line;
   1. Scheduled AMMs.
1. Proximity to create Stake Weighted Oracle and proof services (proof generation UI & backend, proof verification smart contract & UI).
1. NDC to create voting contracts: a) constitution ratification and b) elections.
1. Organize 2 workshops about the process (internal and external).
1. Contract demos.

## Roadmap

![v1 timeline](assets/v1-timeline.png)

## Voting

Voting is happening on chain by the _Voting Body_: the NEAR Ecosystem general assembly for elections, referendums, and voting comprised of every NEAR Account (account) designated as a voting account.
For v1, the Voting Body is set of accounts staking NEAR, except staking pools and other identified entities who are known to aggregate stake.

### Constitution

Constitution Proposal will provide 3 options: `yes`, `no` and `abstain`. The reason we are including abstain is to make the quorum more meaningful: people who don’t want to take a side (yes / no) but want to be counted into the quorum can do so. For example, if the NEAR Foundation doesn’t want to vote yes/no, but want to support the initiative, then NF can vote abstain.
The proposal passes if both conditions below are met:

- Quorum = 8%: means that sum of all voted stake

        #yes + #no + #abstain>= 0.1 \_ total_staked_near

- Threshold = 60%: means that:

        #yes > 0.6 \_ (#yes + #no)

Example of a proposal passing (assuming there are 500 stake in total):

    yes=65stake, no=35stake, abstain=10
    yes=8stake, no=2stake, abstain=50

Example of a proposal NOT passing (assuming there are 500 stake in total):

    yes=60stake, no=40stake, abstain=any – didn’t pass the threshold
    yes=8stake, no=2stake, abstain=20 – not enough quorum

## Transparency Comission

TODO: provide process of electing transparency comission
