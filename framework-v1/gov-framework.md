# A Framework for the Governing Bodies of the NEAR Digital Collective

| Version: | Date:             | Status:                                            |
| -------- | ----------------- | -------------------------------------------------- |
| v1.2     | June 2, 2023      | Publicly Visible to NDC                            |
| v1.3     | October 1, 2023   | Release Candidate                                  |
| v1.4     | November 14, 2023 | Full Release                                       |
| v1.4.1   | November 23, 2023 | Fixes, reconciliation and added `min_vote_duration` |

## Summary

There are four governing bodies of the NDC Governance Framework. Each governing body has specific roles and capabilities such that a system of checks and balances can develop. The role and powers vested in these different governing bodies provide a robust framework for ensuring governance of the Community Treasury in line with NEAR values and the ecosystem objectives.
At a high level, the balance of powers between these governing bodies can be understood in the following manner:

### Voting Body

All non-blacklisted human verified (using [I Am Human (**IAH**)](https://i-am-human.app/)) accounts. There are no requirements for being a member of the voting body beyond possession of 'I am Human' face verification SBT and not being in the [blacklist](https://near.org/neardigitalcollective.near/widget/NDCDocs_OneArticle?articleId=Election_Integrity%E2%80%94Voter_Verification_Update&blockHeight=100436088&lastEditor=neardigitalcollective.near).

### Council of Advisors

Role: Advise and Block.

While the Council of Advisors sits in support of the HoM and maintains the ability to block a proposal or removal request, they are beholden to the HoM for the passage of proposals. Meanwhile, they are also beholden to the Transparency Commission insofar as they cannot remove members or investigate them.

### House of Merit

Role: Propose and Allocate.

While the HoM has the ability to propose legislation proactively, they are beholden to the Council of Advisors and ongoing checks if poor leadership is repeated over time. In the same vein, they are also accountable to the Transparency Commission in terms of ethics and transparency of their role.

### Transparency Commission

Role: Investigate and Remove.

While the Transparency Commission commands the sole power of hearing complaints, investigating members of both the HoM and the CoA, and to either extend an investigation, retain a member after investigation, or remove that member as a result of the investigation. CoA has the ability to allow someone who has been removed from their post to run for future sessions, only after they have been removed.

### Notes

All three institutions elect speakers at the beginning of each congress, and all institutions are required to meet weekly - with the HoM required to meet every 2 - 3 days.

As this system evolves, each governing body has the ability to both support and limit the actions of the adjacent governing bodies. In this manner, while the system will evolve every election cycle with new members, the system itself will retain its functionality.

### House Voting Criteria

In this section we describe HoM, CoA and TC voting mechanism.

Each house has the following voting parameters:

- `approval_threshold`: minimum amount of approvals cast during the voting period to approve a proposal.
- `vote_duration`: maximum amount of time a proposal is active for voting.
- `min_vote_duration`: minimum amount of time a proposal is active for voting, unless all members voted. This parameter is introduced to let other members vote (and express their opinion) even if the voting result is already established.
- `cooldown`: additional amount of time to hold off proposal approval. It's used to give extra time for veto motion.

A proposal, when created, is immediately active for voting until:

- all voters voted;
- or `min_vote_duration` didn't pass and voting is result is not established;
- or `min_vote_duration` passed and voting result is established.
- or `vote_duration` is over.

When a proposal is active, any member can vote to approve, reject or abstain.

Cooldown (if non zero) starts once proposal is got at least `approval_threshold` votes and the proposal is not active. Cooldown will block the proposal to be executed, to give a authorized parties to veto it.

**Approval Criteria**:
Vote to motion passes once `approval_threshold` votes in favor AND cooldown passed without any veto from authorized party.

**Rejection Criteria**:
Not receiving `approval_threshold` votes in favor nor veto from CoA (where relevant). If a proposal gets enough rejection and abstain votes to make approval not possible, then it will be rejected.

**Tie Breaking**:
No Tie is possible. If a member is removed prior to next election, then a hard majority of `approval_threshold` votes in favor must still be obtained, and grid-locked is taken as a rejected Motion.

## Council of Advisors (CoA)

> **Processes & Procedure = Supportive, Defensive**

<aside>
⚠️ TL;DR: The Council of Advisors is responsible for advising, publicly prioritizing, and in cases of recurring issues, blocking actions of the two different governing bodies.

The Council of Advisors operates on a _weekly time frame_ where their primary activities are to:

1. Set Priorities for the HoM,
2. Evaluate HoM , and
3. Vote to Motion
   1. against any HoM proposal,
   1. against an implemented proposal,
   1. overturn a TC ban and unban the member's eligibility to run in subsequent elections.

TC can dismiss any member from any house (including from TC itself), and moreover ban (`GovBan` I Am Human flag).
CoA can unban a member (remove `GovBan`flag) at any time to run for future sessions (it will NOT bring him back to the office in the existing term).

</aside>

**Membership:** 7 members.

**Total Terms:** Max of 2 terms per individual.

**Tenure per Term:** 6 months.

**DAO Parameters:** `approval_threshold = 4, vote_duration = 5 days, min_vote_duration = 3 days, cooldown = 0 days`

**Appointment Eligibility Criteria:** Satisfying [OG SBT](https://near.org/neardigitalcollective.near/widget/NDCDocs_OneArticle?articleId=NDCV1-Safeguards&OGSBT&blockHeight=96512909&lastEditor=vikash.near) criteria.

**Removal Criteria:** Complaint and investigation from filing to TC followed by a motion to remove.

**Salaries**: (Based on contribution level)

1. Speakers and core contributors to each house will generally contribute more hours; some part-time and full-time resources may be required.
2. Hours vary based on representative availability, proposal volume, and process definition needs.

### Processes, Timelines & Key Stakeholders

| Process                                          | Description                                                                                                                                                | Time Frame                            | Key Stakeholders   |
| ------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------- | ------------------ |
| Motion to Veto the Setup Package                 | Either expedite the passage (approve), or veto the passage of the new congress’ setup package                                                              | 3 days to 1 month per vetoed proposal | CoA, HoM           |
| Motion to Veto an Active or Implemented Proposal | Vote to veto a passed proposal from the House of Merit                                                                                                     | 3 days to 1 month per vetoed proposal | CoA, HoM           |
| Formally Set Priorities for Congress             | Clarify the priorities the Council sees as most important, and to indicate what types of proposals may be most or least successful                         | As needed                             | CoA                |
| Evaluate Performance of Governance Bodies        | Signal to the voting body the performance of both the House of Merit and the Transparency Commission, or to jolt either house to improve their performance | As needed                             | CoA, Voting Body   |
| Unban members, banned by TC                      | Ability to re-instate banned members                                                                                                                       | As needed                             | CoA, Banned Member |

### Minimum Threshold of Engagement for CoA

| Activity            | Minimum Threshold | Frequency    | Implication of Failure | Notes                              |
| ------------------- | ----------------- | ------------ | ---------------------- | ---------------------------------- |
| Meeting Attendance  | 60%               | Per Month    | Subject to Removal     | Required to maintain active status |
| Voting on Proposals | 70%               | Per Proposal | Subject to Removal     | Required to maintain active status |

The Council of Advisors operates on a weekly time frame. The essence of their job is to help the HoM set ecosystem priorities in parallel to evaluating HoM and TC performance for the month prior. In the event that there is a divergence in HoM operations and the vision of the CoA, they are able to motion to block a proposal or policy from the HoM. This motion to block can take place during and/or after a proposal or action has been taken by the HoM.

**Timeframe: Weekly**.

### Proposals and Voting

At least `approval_threshold` approvals are required to pass a proposal. This structure ensures that the Council of Advisors serves primarily as a safeguard against ill-advised decisions, rather than as an active governing body in the governance and implementation of proposals.

- Veto a HoM proposal:
  - veto must be approved by CoA before the HoM proposal cooldown finishes.
- Vote against an implemented proposal and vote to appeal and overturn a TC ban and unban the member's eligibility to run in subsequent elections.
  - Can be proposed at any time.
- Overturn a TC ban. TC can remove a member from the office - that member is ineligible to serve for the remainder of that term. However, they may run in future elections. Additionally, TC can decide to ban a member from running in future elections, the member's OG SBT is burnt and the members is flagged with `GovBan` flag, rendering them ineligible for future candidacy.
  **Appeal Process to the CoA**:
  - Banned members have the right to appeal their ban to the CoA.
  - If the CoA finds in favor of the appealing member, the following technical process is initiated: a new OG SBT is minted for the member and `GovBan` flag is removed, reinstating their eligibility to run in subsequent elections.

#### Appeal Process

No appeal. Simply requires a re-submission of the vote to motion.

### Ongoing Activities

- Release Priorities for the Ecosystem for HoM.
- Release Evaluation of Activities from HoM and TC.
- Motion to block or overturn ongoing or existing decisions or policies.

## House of Merit (HoM)

> **Processes & Procedure = Active, Directive**

<aside>
⚠️ *Tl/Dr: T*he House of Merit is responsible for proposing, passing, and allocating **Funding Proposals** from the NEAR Treasury within an agreed-upon Budget Package agreed with the CoA, to hire or create new roles for the NDC itself, and to alter any protocol governed mechanics or public goods. The HoM is the primary engine of policy implementation and budget allocation for the governance of the NEAR Ecosystem. The HoM operates on a *weekly* timeframe, whereby a proposal is voted on. In order for a proposal to be implemented it requires a hard majority of 8 votes in the HoM and for the not being vetoed.

</aside>

**Membership:** 15 elected members (or less, if a member has been removed).

**Total Terms:** Max of 2 terms per individual.

**Tenure per Term:** 6 months.

**DAO Parameters:** `approval_threshold = 8, vote_duration = 5 days, min_vote_duration = 3 days, cooldown = 7 days` . Cooldown allows CoA and VB to veto a proposal during the proposal voting and after 7 days after a proposal passed. The proposal can’t be executed after the cooldown is over.

**Appointment Eligibility Criteria:** Satisfying [OG SBT](https://near.org/neardigitalcollective.near/widget/NDCDocs_OneArticle?articleId=NDCV1-Safeguards&OGSBT&blockHeight=96512909&lastEditor=vikash.near) criteria.

**Removal Criteria:** Complaint and investigation from filing to TC followed by a motion to remove.

**Salaries**: (Based on contribution level)

1. Speakers and core contributors to each house will generally contribute more hours; some part-time and full-time resources may be required.
2. Hours vary based on representative availability, proposal volume, and process definition needs.

### Processes, Timelines & Key Stakeholders

| Process                                     | Description                                                                          | Time Frame                                                       | Key Stakeholders |
| ------------------------------------------- | ------------------------------------------------------------------------------------ | ---------------------------------------------------------------- | ---------------- |
| Proposal of the Congressional Setup Package | Defines budget, 'big budget item', 'recurring item' and procedural timers            | Start of every congress                                          | HoM              |
| Proposal for Budget Allocation              | Proposes the deployment of the congressional budget for a specific ecosystem purpose | Date is set by Proposer and vote is open for 5 days per proposal | HoM              |
| Proposal for Gov Framework Change           | Modifies the Gov Framework or an element of the governance framework                 | Date is set by Proposer and vote is open for 5 days per proposal | HoM              |
| Proposal for Official Long Term Strategy    | Votes on the priorities and strategies of the Congress                               | Date is set by Proposer and vote is open for 5 days per proposal | HoM              |
| Proposal to Hire                            | Creates and funds a position in the NEAR Ecosystem for a specific role               | Date is set by Proposer and vote is open for 5 days per proposal | HoM              |

### Minimum Threshold of Engagement for HoM

| Activity            | Minimum Threshold | Frequency    | Implication of Failure | Notes                              |
| ------------------- | ----------------- | ------------ | ---------------------- | ---------------------------------- |
| Meeting Attendance  | 60%               | Per Month    | Subject to Removal     | Required to maintain active status |
| Voting on Proposals | 70%               | Per Proposal | Subject to Removal     | Required to maintain active status |
| Proposal Creation   | 2                 | Per Term     | Subject to Removal     | Required to maintain active status |

The HoM is required to meet every 2 to 3 weekdays at minimum. This allows the HoM to move quickly and iterate efficiently. Any HoM member can make a proposal and put it into motion. 8 votes in favor is required to pass. The voting period for all votes last for 5 days once they are proposed (the proposal creator decides when they are proposed).

Timeframe:

- Meetings at least every 2 to 3 weekdays
- Voting is on-going and asynchronous.

### Budget **Package - 1st Order of Business:**

| Line Item Code | Main Category                                                   | Subcategory Code | Subcategory             | Purpose                                | Rationale                              | Budget Allocation |
| -------------- | --------------------------------------------------------------- | ---------------- | ----------------------- | -------------------------------------- | -------------------------------------- | ----------------- |
| HOM-001        | Main Category 1: Brief description or purpose of this category. | XXX-001A         | Specific Initiative 1.1 | Describe the specific purpose or goal. | Explain the reason or logic behind it. | $Allocation       |
|                |                                                                 | XXX-001B         | Specific Initiative 1.2 | Describe the specific purpose or goal. | Explain the reason or logic behind it. | $Allocation       |
| HOM-002        | Main Category 2: Brief description or purpose of this category. | XXX-002A         | Specific Initiative 2.1 | Describe the specific purpose or goal. | Explain the reason or logic behind it. | $Allocation       |
|                |                                                                 | XXX-002B         | Specific Initiative 2.2 | Describe the specific purpose or goal. | Explain the reason or logic behind it. | $Allocation       |
| HOM-003        | Main Category 3: Brief description or purpose of this category. | XXX-003A         | Specific Initiative 3.1 | Describe the specific purpose or goal. | Explain the reason or logic behind it. | $Allocation       |
|                |                                                                 | XXX-003B         | Specific Initiative 3.2 | Describe the specific purpose or goal. | Explain the reason or logic behind it. | $Allocation       |
| HOM-004        | Main Category 4: Brief description or purpose of this category. | XXX-004A         | Specific Initiative 4.1 | Describe the specific purpose or goal. | Explain the reason or logic behind it. | $Allocation       |
|                |                                                                 | XXX-004B         | Specific Initiative 4.2 | Describe the specific purpose or goal. | Explain the reason or logic behind it. | $Allocation       |
| HOM-005        | Main Category 5: Brief description or purpose of this category. | XXX-005A         | Specific Initiative 5.1 | Describe the specific purpose or goal. | Explain the reason or logic behind it. | $Allocation       |
|                |                                                                 | XXX-005B         | Specific Initiative 5.2 | Describe the specific purpose or goal. | Explain the reason or logic behind it. | $Allocation       |

---

At the beginning of every new congress, the first order of business is for the HoM to create and propose a new **Budget Package**. This package defines the budget for the upcoming **Congress**:

- Budget for the current **Congress**.
- Agreement between CoA and HoM on what to spend funds on.
- Must be created within the confines of the most recent valid Setup Package (which would typically have been proposed by the previous congress and recently have been approved during the election period).
- Typically contains line items for each Constellation and Node, with monthly projected spend for each line item.
- Note: The budget in v1 is a text based document. For this reason, Funding Proposals will require manual / off-chain validation against the budget.

The HoM must also elect a Speaker at the beginning of each Congress. The Speaker is in charge of setting and running meetings of the HoM, deciding which topics are to be covered or require further discussion in order to optimize the institution's efficiency. The Speaker can be replaced during a Congress following a vote of no-confidence.

<aside>
⚠️  note that they HoM can propose to change params of the existing session. It’s going to be done as a Text proposal, and requires a Voting Body approval. That means, once HoM approves new budget with new params, the HoM must propose to VB to ratify this change.

</aside>

HoM can’t change the following params:

- Cap Budget Item: maximum value of the single proposal.
- term limit → DAO must have “end time”.
- recurring budget item max size = 6 months. It's an item that is processed sequentially on the interval by the trust (renews automatically without another vote by the HoM or check by CoA). Vetoing it doesn’t have additional tech callback - it’s processed by trustees.
- session budget: max budget they can operate.

HoM can change the following params:

- `hom.big_budget_size = 75k USD` (initial one). It is set by the HoM and it is for them to define what items of size they would like to set as thresholds for VB checks,

The initial parameters are defined by the _Initial Setup Package_, which is voted by the Voting Body during Elections.

### Setup Package - Last Order of Business

<aside>
⚠️ this is not implemented and will require approval from HoM to implement it.
</aside>

[Setup Package Overview](https://www.notion.so/Setup-Package-Overview-6df6ec7ac92d4703af1fee4a89c61da1?pvs=21)

At the end of every **Congress**, the last order of business is for the HoM to create and propose a new **Setup Package** . This package defines the following for the next **Congress**:

- Total budget cap for the next congressional period.
- Threshold (amount) for a **Funding Proposal** to be deemed a ‘big budget policy’.
- Threshold (amount) for how much any one recipient / Constellation / Node can receive in a month.
- Procedural changes to timers or cycles (after the first session).
- Changes to the composition and function of the HoM, CoA, or TC.

This **Setup Package** sets the precedent for how the new **Congress** will operate. Only after the **Voting Body** has passed the **Setup Package** does the HoM commence operations.

### Proposals

Proposal lifetime: `created → HoM voting → cooldown`.

CoA has veto power over all active or recurrent proposals.
Voting Body has veto power over Funding Proposals above the big budget threshold value and Recurring Funding Proposals.

#### Setup Package

A **[Setup Package](https://www.notion.so/Setup-Package-Overview-6df6ec7ac92d4703af1fee4a89c61da1?pvs=21)** can be proposed by any member in either the HoM or CoA, and must then pass a simple majority by the **Voting Body** in a general election, before being implemented (1 week implementation time). A minimum of 1 **Setup Package** must be proposed prior to a general election.

- If one **Setup Package** has been proposed, then it will be a approve or reject or abstain vote which must pass with a simple majority, i.e. more votes in favor than votes against, by the **Voting Body** in a general election.
- If more than one **Setup Package** has been proposed then voters in the **Voting Body** will be given one vote each and can cast it either in favor of the **Setup Package** that they prefer, or can abstain. The **Setup Package** with the most votes in favor wins.
- General elections are subject to an 8% quorum requirement, inclusive of any “abstain” votes cast.

#### Funding Proposal

- Each **Funding Proposal** must first fit within the confines of the parameters defined in the **Setup Package** before it can be created. The Smart Contract will validate and enforce these rules and will not allow creation of a **Funding Proposal** that violates the **Setup Package**.
- Recurring **Funding Proposals,** and one-off **Funding Proposals** above the big budget threshold value, require 8 votes in favor in the HoM, and then a subsequent CoA approval.
- Non recurring **Funding Proposals** below the big budget threshold value require 8 votes in favor in the HoM and the absence of a CoA veto.

#### Budget Proposal

- Require HoM [approval](#house-voting-criteria) in favor in the HoM, and then a subsequent CoA approval.

#### Proposal to change gov mechanics

Require Voting Body approval with **Near Supermajority Consent**.

#### Other proposals

HoM can make Text based proposals. That should cover all proposals that don't require additional VB approval and are not covered above. Example: long term strategy (focus), hiring etc...:

### Appeal Process

Re-proposal the following week.

### Growth

After the first congress, 2 new members are added to the House of Merit each Congress, until there are 31 members total. The threshold to pass a vote is simultaneously increased by one, until the threshold reaches 16.

## Transparency Commission (TC)

> **Processes & Procedure = Investigate and Remove**

<aside>
⚠️ Tldr:The Transparency Commission (TC) is responsible for maintaining proper procedure and governance of the NDC for the benefit of the ecosystem. This applies on four levels: (1) For initiate and (or) the removal of any poor actors violating codes of conduct or acting out of self-interest, (2) For the removal of any member from a complaint of incompetence, (3) For qualifying candidates looking to run for a seat in any of the governing bodies. (4) Guaranteeing transparency of operations and intentions with the community, including oversight of fund distribution and evaluation of integrity of stakeholders. During the congressional term, the Transparency Commission is in charge of listening to, selecting complaints, and investigating them, from which only the TC can decide to either extend (the investigation), remove the member, or retain the member. Notably, the members of the TC themselves cannot file a complaint - they are tasked with investigating the complaints from the ecosystem after carefully evaluating their merit and legitimacy.

</aside>

**Membership: 7** members.

**Total Terms:** Max of 2 terms per individual.

**Tenure per Term:** 6 months.

**DAO Parameters:** `approval_threshold = 4, vote_duration = 5 days, min_vote_duration = 3 days, cooldown = 0`

**Appointment Eligibility Criteria:** Satisfying [OG SBT](https://near.org/neardigitalcollective.near/widget/NDCDocs_OneArticle?articleId=NDCV1-Safeguards&OGSBT&blockHeight=96512909&lastEditor=vikash.near) criteria.

**Removal Criteria:** Complaint and investigation from filing to TC followed by a motion to remove.

**Salaries**: (Based on contribution level)

1. Speakers and core contributors to each house will generally contribute more hours; some part-time and full-time resources may be required.
2. Hours vary based on representative availability, proposal volume, and process definition needs.

### Processes, Timelines & Key Stakeholders

The transparency commission meets to evaluate complaints, issue public opinions on such complaints, or issue notice of investigation. Every investigation may last as much as needed. Both the HoM and the CoA respect the final verdict of the TC; however, the CoA does possess the ability to clear or reinstate (to run once again) a dismissed individual.

As a matter of operations, the TC must investigate complaints against themselves.

Timeframe: To go over complaints and initiative investigations. Investigations limit = no limits.

| Process               | Description                                                                                            | Time Frame                                     | Key Stakeholders               |
| --------------------- | ------------------------------------------------------------------------------------------------------ | ---------------------------------------------- | ------------------------------ |
| Motion to Investigate | Open an investigation to a complaint against an individual elected to an NDC body                      | As needed, duration of investigation as needed | TC, Member under investigation |
| Motion to Remove      | Removes a member from the post, leaving the post empty until the next election cycle                   | As needed                                      | TC, Member being removed       |
| Motion to Ban         | Removes a member from the post, and bans that member from serving in ANY Governance post in the future | As needed                                      | TC, Member being banned        |

### Minimum Threshold of Engagement for TC

| Activity            | Minimum Threshold | Frequency    | Implication of Failure | Notes                              |
| ------------------- | ----------------- | ------------ | ---------------------- | ---------------------------------- |
| Meeting Attendance  | 60%               | Per Month    | Subject to Removal     | Required to maintain active status |
| Voting on Proposals | 70%               | Per Proposal | Subject to Removal     | Required to maintain active status |

### Proposals

Members of the TC receive complaints and requests for investigation. Once a request is successfully considered, TC can make one of the following on chain proposals:

- **Motion to Remove / Revoke Powers**: A proposal to dismiss the member of their current role and responsibilities.
- **Motion to Remove and Ban**: A proposal to not only remove the member from their role but also ban them from future participation.
  - This is done manually by removing OG.
- **Motion to Retain**: A proposal to keep the member in their current role and end the investigation without further action

#### Appeal Process

The only appeal (for motion to remove and ban) process can be done through the CoA for a motion to Remove and Ban after two months and a strong majority vote or within the TC itself, pending another investigation.

### Investigation on a member of the TC

In the event a member of the TC is under investigation, they are ineligible to vote on the motion to investigate them or any subsequent motion related to it. Specifically, they cannot participate in votes that concern their own status. The TC defines the scope of votes that can concern a member. The complete list of proposals that can concern a member includes:

- Dismissal of the member under investigation
- Banning the member from future participation

However, until that member is either removed or retained, they may vote on any other issue. In the event of resignation prior to re-election, any grid-locked decision is taken as a rejection of the proposal.

## The Voting Body

### Quorums and Thresholds

- **Near Consent:** quorum=(7% of the voting body) + **simple majority**= `#yes > 50% * (#yes + #no + #spam)`.
- **Near Supermajority Consent**: quorum=(12% of the voting body) + **super majority**= `#yes > 60% * (#yes + #no + #spam)`

### Powers and Responsibilities

- Elect members of institutions every 6 months.
- Dissolve institutions deemed incompetent.
- Amend the Governance Framework.
- Veto Big budget items over a certain threshold.
- Veto any recurring budget items.
- Vote on matters related to the Community Treasury, including:
  - Swapping NEAR Consent for NEAR Supermajority Consent.
  - Changes to NEAR Supermajority Consent & Quorum requirements.
  - Overriding powers.
  - Addition & Exclusion of trustees.
  - Amend trust instrument.
  - Make distributions.
- Ratify Setup packages.

### Processes, Timelines & Key Stakeholders

| Process                                                          | Description                                                              | Votes required             | Time Frame            |
| ---------------------------------------------------------------- | ------------------------------------------------------------------------ | -------------------------- | --------------------- |
| Election                                                         | Vote for members to serve in each institution                            |                            | 1 week every 6 months |
| Dissolve Institutions                                            | Vote to dissolve any of the institutions                                 | Near Supermajority Consent | As needed             |
| Amend the Gov Framework                                          | vote to amend the constitution or an element of the governance framework | Near Supermajority Consent | As needed             |
| Veto Large Budget Items                                          | Vote to veto budget items over a certain threshold                       | Near Consent               | As needed             |
| Veto Recurring Budget Items                                      | Vote to veto any recurring budget items                                  | Near Consent               | As needed             |
| Community Treasury - Swapping NEAR Consent                       | Vote to swap NEAR Consent for NEAR Supermajority Consent                 | Near Supermajority Consent | As needed             |
| Community Treasury - Supermajority Consent & Quorum requirements | Vote to changes to NEAR Supermajority Consent & Quorum requirements      | Near Supermajority Consent | As needed             |
| Community Treasury - Overriding powers                           | Vote to Overriding powers                                                | Near Consent               | As needed             |
| Community Treasury - Addition & Exclusion of trustees            | Vote to Addition & Exclusion of trustees                                 | Near Consent               | As needed             |
| Community Treasury - Amend trust instrument                      | Vote to Amend trust instrument                                           | Near Consent               | As needed             |
| Community Treasury - Make distributions                          | Vote to Make distributions                                               | Near Consent               | As needed             |
| Ratify Setup package                                             | Vote to ratify Setup package                                             | Near Consent               | As needed             |
| Approve Budget                                                   | Vote to approve budget proposed by HoM                                   | Near Consent               | As needed             |

The voting process is described in the Voting Body [contract documentation](https://github.com/near-ndc/voting-v1/tree/master/voting_body). In summary:

- Any Voting Body member can create a proposal.
- We need to introduce an anti-spam mechanism. The proposal flow introduces two queues: pre-vote queue (proposals that require more support or congress support before reaching the voting stage) and the active queue (verified proposals, ready for voting). See [creating proposals documentation](https://github.com/near-ndc/voting-v1/tree/master/voting_body#creating-proposals).
- Voting Body proposals are not finalized optimistically. Once in the voting stage, proposals are active until the end of the voting duration. This will give chance all members to express their opinion and provide more valuable result than simple approved / rejected (for example it also interesting to see how many people rejected a proposal even if it was eventually approved).
- In the current implementation, users can overwrite their votes. This decision was made following the elections feedback and motivated by the fact that new analysis about a proposal can come at later stage which can change mind of the voters who voted early on.

### Double Clicking On Dissolving a Governance Body

The threshold to reset an elected Governance Body - and dissolve it for new elections. For any of the three governing bodies, dissolve requires **Near Supermajority Consent**. If this vote is successful, new elections are held for the governing body, with the following week starting the candidacy period (See the governance framework for election timeframes!).

Note, this vote is done for only one governance body at a time - the voting body cannot dissolve all three houses at once. It must be three separate proposals and three separate votes.

### Changes To the Governance Framework

Changes to the governance framework can be made in two ways:

1. Via proposal and passage from the House of Merit, such that it is also NOT Vetoed by the Council of Advisors (in the usual passage).
2. Via the voting body, with **Near Supermajority Consent**. The proposal itself details out the full degree of changes made to the constitution and governance framework.

The changes are then implemented in the next Congress.

### Influence on the NDC

The voting body retains a significant influence over the NDC, ensuring its ability to overturn or shape its performance.
Moreover, Voting Body can be easily used as an authority over any DAO. `FunctionCall` type can call any external contract.
Moreover, we encourage other DAOs to Voting Body as a conflict resolution (could be used using `Text` proposal or aforementioned `FunctionCall` if related hook is available in the DAO).

## The Election Procedure

The election procedure establishes the precedent for how elections are conducted for all three governing bodies. It also pertains to the expansion of the governing bodies and alterations to the Gov Framework over time.

- _Election Eligibility Requirements:_ OG SBT.
- _Eligibility and Announcement:_ During the nomination period.
- _Election Timeframe:_ 2 weeks.
- _Onboarding Process:_ 1 week post-election
- _Conflicts of Interest:_ Community members looking to assume positions should disclose all their relevant affiliations, as well as any other potential conflicts of interest.

The ‘Election procedure’ can be divided into three separate sections:

- _The Candidate Process:_ How a person runs for a position and onboards to that position.
- _The Election Timer:_ When elections are conducted, the timeframes for voting, and the start of a new congress.
- _System Iteration Over Time:_ How these mechanics are able to be changed within the governance framework.

### The Candidate Process

To participate in any of the three governing bodies, a candidate must adhere to the following process:

1. the candidate cannot run for more than one seat in a given election; They must decide to run for either the HoM, CoA, or TC.
2. all candidates must announce their candidacy during the nomination period prior to the election. In the first congress, only OG SBT holders are eligible to run for congress.

Once a candidate has announced their candidacy, fulfilling the relevant OG SBT criteria, they appear on the election ballot voted on by the ecosystem during the election week. For all three institutions, all names are listed in random order, and the names with the most votes fill the open seats - this refers to a ranked-order voting structure, with the winners having the most votes from the field of candidates. In the first congress, there will be 29 open seats.

At the conclusion of the election, the winners are decided based upon majority vote.

1 week after the end of the election, the new candidates onboard to the governance platform and assume responsibilities based upon the seats they have been elected to.

### The Election Timer

The election timer refers to the timeframe for governance congresses and election cycles. Every election and every seat abides by the same election timer.

All candidates must announce their intention to run during the nomination period prior to the election. **The first congressional nomination window opens on July 20th and runs to September 7th.**

As the name suggests, the Election period is a two-week event from which any Verified/Unverfied Account can vote for any nominated candidate if they meet the bonding/or other requirements. **The first congressional election period starts on September 8th and runs until September 22nd (two weeks).**

At the close of the election period, a one-week window onboards the new congress and allows them to elect a speaker and orient themselves. This is known as the ‘setup week’ and is also when the members of the HoM can prepare to present the Setup Package. If changes are made in reference to the election process or timer, this takes place in the following election cycle.

At the end of T-Week the ‘Setup package’ is submitted, and the Congress officially begins. In the event that the Voting Body does not approve the ‘setup package,’ the new congress must submit another setup package for review before any other legislation can be passed or considered.

### System Iteration Over Time

Every new congress has the ability to alter the fundamental mechanics of the governing bodies in the passage of a new setup package. This means that any expansion to a governing, timer or term changes, or procedural change is done at the start of the new congress and implemented for the next election cycle - assuming approval by the CoA.

In addition, the governing bodies can, at any time, based on the feedback of the community and an approved referendum with a Super Majority Vote, be amended or reconstituted, known as a **_reset_** by an amendment to the Gov Framework. While the governing bodies are responsible for managing the community treasury, the voting body maintains the right to ensure the ecosystem continues its journey to decentralization by ensuring that evolving governance models are pragmatically implemented over time.

---

## References

1. [NDC Overview Slides](https://docs.google.com/presentation/d/1YFzsBRB-UcZYN93tDVEHUGE7uGx2OuW61PnXsNMYgPU/edit?usp=sharing)
2. [NDC Trust](https://bafybeic5s7qbf3dlbwqesv4byzc6llwpfx2kq36xzwfknu7sskxlanellm.ipfs.nftstorage.link/)
3. [NEAR Constitution](./constitution.md)
4. [Code of Conduct](https://medium.com/near-digital-collective/ndc-code-of-conduct-89589dd137ba)
5. [Declaration of Transparency and Accountability](https://bafkreid3vx2tivdlwkivezalhkscxnxakirw5nuunxce3b6ivtx4j6ac44.ipfs.nftstorage.link/)
6. [Fair Voting Policy](https://bafkreidwdxocdkfsv6srynw7ipnogfuw76fzncmxd5jv7furbsn5cp4bz4.ipfs.nftstorage.link/)
7. [Product Book](https://docs.google.com/document/d/1w_wfRfp-ISH7g-zu7vAFULVvRNwyLGwNIDC1EBkxvu0/edit?pli=1) (outdated)
8. [Voting Body](https://github.com/near-ndc/voting-v1/tree/master/voting_body) contract implementation.
9. [Congress](https://github.com/near-ndc/voting-v1/tree/master/congress) (HoM, CoA, TC) contract implementation.

### Tools:

- [Astra++](https://near.org/astraplusplus.ndctools.near/widget/home?page=congress) - Congress, Voting Body, DAOs
- [NDC Docs](https://near.org/neardigitalcollective.near/widget/NDCDocs) - post/edit final docs
- [Easy Poll](https://near.org/easypoll-v0.ndc-widgets.near/widget/EasyPoll?page=official_polls) - Community pulse and sentiment
- [NDC Chatbot](https://ndc-chatbot.nearhub.club/) - Ask questions
- [Kudos](https://near.org/kudos.ndctools.near/widget/NDC.Kudos.Main) - appreciation and recognition
