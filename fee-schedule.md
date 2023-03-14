# Fee Schedule

This is a pre-draft of how fees can work for Chaincast, only for reference and debate purposes.

## 2.2 Fee Schedule

Fees are the revenue of the protocol and will be used for sustaining Chaincast and be distributed to Chaincast stakeholders. Fees will also be used as a deterrent against spamming broadcasts by protocols. This is an important factor so as to both keep the flows low for end-users and also promote the consumption of the broadcasts.

Fees will be paid on the Chaincast's governance token "CAST". Temporarily, as the protocol makes its first steps, alternative tokens like USDC may be used.

There are two tiers of fees:

1. "Base Weekly Fee" This fee applies to broadcasts with the "Weekly Update" category.
2. "Base Fee" This fee applies to all other categories.

The purpose of having two tiers of base fees is to have a much lower cost on broadcasting weekly so as to incentivise protocols to post updates to their most engaged members more often.

The exact token values of the Base Fees are beyond the scope of this paper. They will be determined dynamically by [governance][governance] based on market conditions.

### 2.2.1 Fee Escalation and Duration Threshold

To discourage protocols from spamming their end-users and consequently abusing the Chaincast protocol, a "Fee Escalation" system is employed. In summary, this system will penalize the protocol that performs more broadcasts than are allowed between the defined time duration of each broadcast.

The Fee Escalation calculation is as follows:

```
Base Fee * (Excheeding Broadcasts + 1) ^ 2
```

Where "Base Fee" is the base fee of the broadcast and "Excheeding Broadcasts" is the times the protocol has exceeded their broadcast limits.

The "Excheeding Broadcasts" number is calculated from the last broadcast that used the base fee - even if that particular broadcast has been deprecated.

#### Example

Assume the Base Fee is 100 tokens.

- Protocol Alpha makes an "Action Needed" broadcast on 1st of May 2022.
  - The base fee of 100 tokens is applied.
- Protocol Alpha makes a second "Action Needed" broadcast, a week later, on the 7th of May 2022.
  - 7 days are way less than the 180 threshold so the Fee Escalation kicks in and now Alpha Protocol has to pay fees of (`100 * (1 + 1) ^ 2`) 400 tokens.
- Protocol Alpha makes a third "Action Needed" broadcast on the 20th of Aug 2022
  - That is ~110 days after the last base-fee broadcast, which is again less than the 180 threshold so the Fee Escalation kicks again. Alpha Protocol has to pay fees of (`100 * (2 + 1) ^ 2`) = 900 tokens.

Bellow find a table of Fee Escalation for up to 5 consequtive broadcasts violating the Duration Threshold, the Base Fee is considered as 100 tokens for this example:

| Threshold Violations | Broadcast Fee |
| -------------------- | ------------: |
| 1                    |           400 |
| 2                    |           900 |
| 3                    |          1600 |
| 4                    |          2500 |
| 5                    |          3600 |

### 2.2.2 Fee Schedule Disclamers

As Chaincast discovers the right product market fit, the "revenue model" will be one of the most intense topics of iteration and change. We welcome feedback and suggestions from our partners, clients and protocols who want to use Chaincast so as to create a fair and sustainable service for all parties involved.
