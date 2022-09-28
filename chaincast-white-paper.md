# Chaincast White Paper V1

# Abstract

This document describes the Chaincast protocol goals, purpose and functionality.

# 1 Introduction

Chaincast's goal is to bridge the communication gap between DeFi and all decentralized protocols with their stakeholders. Chaincast is a one-way, broadcasting protocol that protocols use to broadcast very important updates about them. Stakeholders can then chose from which protocols they want to receive updates and subscribe to these feeds.

Chaincast is not a governance tool, although it can announce very important governance decisions. Chaincast can act as an emergency broadcast network, directly informing stakeholders about actions they need to take immediately due to a security breach or other urgent reasons.

The stakeholders will have multiple means of consuming the updates, including directly from on-chain, a website, social media, chat and messaging applications, email, SMS and any other convenient medium.

The Chaincast Protocol aspires to be the main hub of information dissimination for all protocols, across all networks and blockchains.

<figure>

![](https://i.imgur.com/gOUhedF.png)

<figcaption align = "center">Figure 1 - Chaincast Overview</figcaption>
</figure>

# 2 The Chaincast Protocol

Chaincast is a decentralized protocol that facilitates one-way communication between other decentralized protocols and their stakeholders.

For each broadcast a fee will be collected and redistributed to the Chaincast's stakeholders according to the tokenomics of Chaincast (CAST) which will be released at a different document and are beyond the scope of this paper.

Broadcasts will be immutable. The contents of the broadcast will be stored on a peer-to-peer hypermedia protocol ( IPFS - [https://ipfs.tech/][ipfs] ), a checksum of the message will be produced and saved on the protocol along with its URL.

The broadcasts will be categorized for finer distribution to interested parties. Different categories will offer varying limits to normal broadcasting fees. For example the "Quarterly Update" category, will allow for 4 base fee broadcasts per year, while the "Emergency" category will only allow 2, beyond those thresholds, the broadcasting fees will increase exponentially.

Stakeholders will have the option to chose from which protocols and which categories in particular they are interested receiving and consuming broadcasts.

## 2.1 Broadcast Core Contract

The **BroadcastCore** contract is responsible for the bulk of the Chaincast's on-chain operations. More specifically it:

- Is responsible for registering new protocols.
- Creates broadcasts.
- Deprecates broadcasts.
- Provides querying functions for broadcast consumption.

The BroadcastCore contract will be upgradeable to facilitate easy and rapid protocol iteration and evolution.

### 2.1.1 Registering New Protocols

To ensure the safety and integrity of the Chaincast protocol as well as the partnering protocols, the new protocol registration will employ a verification process. The goal is to ensure that the protocol requesting to register is the official one.

Upon registration an address or set of addresses will be added to the allowed list to post broadcasts on the behalf of the registering protocol.

### 2.1.2 Broadcasting

Broadcasting will require the following inputs:

- URL to the broadcast message (on IPFS).
- Checkshum SHA256 of the message.
- Category selection.

The broadcasting fee will be collected according to the [Fee Schedule][fee-schedule].

Broadcast messages are expected to be in [Markdown format][markdown]. While there is no way for a smart-contract to validate this, it is a convention that must be complied with to promote interoperability of the distribution systems.

### 2.1.3 Broadcast Deprecation

To account for mistakes or newer updates emerging, a deprecation operation will exist. Deprecation will require:

- Broadcast ID that will get deprecated.
- The new Broadcast ID.

Deprecation will result in the deprecated message not be visible on normal queries.

Deprecation will collect the base fixed fee.

### 2.1.4 Broadcasting Categories

Categories define the type of the broadcast, help stakeholders consume the kind of messages they are interested in and allow for custom attributes and behaviours for the broadcasting messages.

Each category will be described by the following properties:

- The ID of the category.
- The name of the category.
- Duration Threshold.

The "Duration Threshold" is expressed in days and dictates the days that need to pass from the last broadcast before the Base Fee can apply again. More information about how this works and fees are calculated on the [Fee Schedule][fee-schedule].

Chaincast will have the following categories:

|  ID | Name          | Duration Threshold | Notes                                                                        |
| --: | ------------- | -----------------: | ---------------------------------------------------------------------------- |
|   1 | Weekly Update |                  7 | Weekly updates for the most engaged stakeholders.                            |
|   2 | Quarterly     |                 85 | Quarterly update of the project.                                             |
|   3 | Emergency     |                180 | An emergency has happened that requires immediate attention and / or action. |
|   4 | Action Needed |                180 | A significant protocol change that requires stakeholder action.              |
|   5 | Vote Needed   |                180 | A significant governance vote that requires stakeholder participation.       |

### 2.1.5 Querying and consuming

Querying for broadcasts is one of the core functions of the Chaincast protocol. As such, querying needs to be versatile and powerful. The following criteria will be available to query for broadcasts, alone or in combination:

- Protocol IDs.
- Category IDs.
- Offset of records.
- Limit of records.

## 3 Fee Schedule

Fees are the revenue of the protocol and will be used for sustaining Chaincast and be distributed to Chaincast stakeholders. Fees will also be used as a deterrent against spamming broadcasts by protocols. This is an important factor so as to both keep the flows low for end-users and also promote the consumption of the broadcasts.

Fees will be paid on the Chaincast's governance token "CAST". Temporarily, as the protocol makes its first steps, alternative tokens like USDC may be used.

There are two tiers of fees:

1. "Base Weekly Fee" This fee applies to broadcasts with the "Weekly Update" category.
2. "Base Fee" This fee applies to all other categories.

The purpose of having two tiers of base fees is to have a much lower cost on broadcasting weekly so as to incentivise protocols to post updates to their most engaged members more often.

The exact token values of the Base Fees are beyond the scope of this paper. They will be determined dynamically by [governance][governance] based on market conditions.

### 3.1 Fee Escalation and Duration Threshold

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

### 3.2 Fee Schedule Disclamers

As Chaincast discovers the right product market fit, the "revenue model" will be one of the most intense topics of iteration and change. We welcome feedback and suggestions from our partners, clients and protocols who want to use Chaincast so as to create a fair and sustainable service for all parties involved.

### 3.3 Fee Distribution

The collected fees will be distributed according to the Tokenomics document and rules and are beyond the scope of this paper.

## 4. Governance

Governance of the Chaincast protocol will happen in a decentralized manner and will dictate all aspects of the protocol. This paper itself is going to be a "living document" residing on a distributed versioning control system (git) and can be amended as per governance decisions.

In particular, the scope of governance includes:

- The "Goals and Purpose" of the protocol.
- The Protocol specifications and requirements.
- Amending the Broadcast Categories.
- Amending the Fee Schedule and Base Fees.
- Tokenomics.
- Delegation of decision making power to committees or partners.
- Ratifying agreements with partners for protocol and service maintenance.
- Amending the governance model.

The exact Governance model, processes and procedures will be described in a dedicated Governance Paper.

## 5. Conclusions

The **Chaincast Protocol** helps decentralized protocols inform and alert their stakeholders. It does so in a decentralized, non-custodial manner while allowing end-users to consume the broadcasts in as many ways and through as many media they feel comfortable with.

The core value proposition of the Chaincast protocol is that it allows end users to get the information, updates and alerts they are looking for from one place. As such, it becomes a requirement for the Chaincast Protocol to exist on one network only, serving protocols from all other Layer 1 and Layer 2 networks. Cloning the Chaincast protocol or having multiple instances on alternate networks fundamentaly breaks the value proposition and nullifies the goal and purpose of the protocol.

The Chaincast Protocol aims to be a stepping stone and fundamental block in the proliferation and adoption of Decentralized Protocols.

[fee-schedule]: #3-fee-schedule
[markdown]: https://www.markdownguide.org/basic-syntax/
[ipfs]: https://ipfs.tech/
[governance]: #4-governance
