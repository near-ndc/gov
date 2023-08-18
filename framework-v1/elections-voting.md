# Elections Voting Process

1. https://miro.com/app/board/uXjVMw-RZnM=/
2. TODO: add more docs

## Voting Process

See [Elections](./README.md#Elections) for general overview of the Nominations and Elections Process.

1. Prior to the elections start, the Elections Commission will setup 4 proposals with correct list of candidates, start time, end time and cooldown period:
   - HoM elections
   - CoA elections
   - TC elections
   - Setup Package approval. TODO: needs more details.
1. Once the proposals are active (between start and end time), each [eligible voter](#eligible-voters) can cast only one vote per proposals. Votes can not be updated nor recasted.
   - when casting a vote, voter must [bond](#bonding) NEAR.
   - voter must pay for all storage fees
1. According to the [safeguards](./README.md#safeguards), Elections Commission will be empowered to revoke any vote which violates Fair Voting Policy. Votes can be revoked any time between proposal.start and proposal.end + cooldown period. Revoked vote can't be recast.
   - Elections Commission will be able to blacklist any user. Everyone will be able to revoke a vote of the blacklisted user by using `iah_registry.is_human_call`.
     More specifically, elections contract will provide a `revoke_vote` method which will allow the Elections Commission or `iah_registry` to revoke the cost. In the latter case anyone can trigger the call and the blacklist check will be required.
1. Elections ends after the cooldown period. At this time, results can be queried from the smart contract.

NOTE: Proposals and candidates can only be submitted by the Elections Commission, following the process approved by the community. Candidates must come from the nominations contract.

### Elections End

The Elections contract must have a final end time, which will be a max of `proposal.end + proposal.cooldown + 1 day` for every proposal added to elections. The extra 1 day is required to give a time to setup the tie break.

## Tie Break

- Only matters if there is a tie at the very tail.
- Options: a) extend number of seats, b) reduce number of seats, c) tie break session - elections only for people at tie.
  - Tie break session with reduced voting period (eg 2 days)

In case of a Tie Break, the elections period will be extended and new proposals will be added by the Elections Commission to setup the tie break.

## Bonding

Each voter must firstly bond **3N** to cast their vote. One bond is enough to cast votes for all proposals. This bond is a safeguard, and will be slashed during the `vote_revoke`, when the voter violates Fair Voting Policy.

Bonding will be integrated in the voting procedure and the contract must return attached tokens (minus the storage fees) if a voter already bonded the tokens.

### I Voted SBT

The Elections contract will act as an issuer for the IAH Registry.

Once the elections are [over](#elections-end) anyone will be able to recover his bond and claim `I_Voted` SBT by calling `elections.unbond` method. The contract will return the bonded NEAR minus storage fees required to mint the `I Voted` SBT.

## Eligible Voters

Any person with a Face Verified Soul Bound Token (SBT) is eligible to vote, and anyone can get one with a NEAR wallet through I-AM-HUMAN.

TODO: other criteria that are discussed:

- staking
- bonding
- activity
