# Stake Weighted Voting

**Status: Draft**

Each account has a variable voting power determined by the amount of NEAR staked at the block height specified in a proposal. Instead of one account = one vote credit, which is gameable in pseudo anonymous world of blockchains (accounts are easy to forge, a proper solution will require human gating mechanism, which is part of the v2 Framework), each account will cast power vote.

The system is being built collaboratively by Proximity Labs and the GWG.

For v1, the Voting Body is set of accounts staking NEAR (delegated to validators), except staking pools and other identified smart contracts and entities who are known to aggregate stake.

- 1 Staked NEAR = 1 vote;

### Stake-Weighted Thresholds

- **NEAR Quorum Requirement** means, in respect of a vote, that votes are cast by the holders of at least `5%` of all Staked NEAR on the NEAR Blockchain.
- **NEAR Big Quorum Requirement** means, in respect of a vote, that votes are cast by the holders of at least `8%` of all Staked NEAR on the NEAR Blockchain.
- **NEAR Consent** means the approval of a proposal (including a Community Proposal), matter and/or decision by the NEAR Community, where a vote of the NEAR Community in relation to that proposal (including a Community Proposal), matter and/or decision takes place and both of the following apply in respect of that vote:
  - the NEAR Quorum Requirement is met;
  - the number of "yes" votes cast is more than 50% of the sum of "yes" and "no" votes: `#yes_votes > #no_votes` (we don't consider abstain votes for the threshold).
- **NEAR Supermajority Consent** -- similar to Supermajority Consent:
  - the NEAR Big Quorum Requirement is met;
  - the number of "yes" votes cast is more than 60% of the sum of "yes" and "no" votes: `#yes_votes > 60% × (#yes_votes + #no_votes)` (we don't consider abstain votes for the threshold).

### Personhood Voting with Stake Weight Quorum Thresholds

- **NDC Approved Account**: has the same meaning as in _Proof-of-Personhood Voting_ above.
- **NEAR Quorum Power** is the sum of cubic root of the staked NEAR of each voting NDC approved account that had staked at the time pointed the proposal (resolved as a snapshot).

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
- **NEAR Supermajority Consent** and **NEAR Consent** have the same meaning as in _Proof-of-Personhood Voting_ above.
