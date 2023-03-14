# Chaincast White Paper V1

# Abstract

This document describes the Chaincast protocol goals, purpose and functionality.

# 1. Introduction

Chaincast's goal is to help all decentralized protocols ("DAOs") keep their stakeholders informed. It is a one-way broadcasting protocol that DAOs use to communicate updates about them. Stakeholders can chose from which protocols they want to receive updates, what kind of updates they want to receive and subscribe to these feeds.

Chaincast can be used to broadcast daily briefs, governance upcoming votes and decisions and important updates of a DAO. It can also act as an emergency broadcast network, directly informing stakeholders about actions they need to take immediately due to a security breach or other urgent reasons.

The stakeholders will have multiple means of consuming the updates, like directly from on-chain, a website, social media, chat and messaging applications, email, SMS and any other convenient medium.

The Chaincast Protocol aspires to be the main hub of information dissimination for all protocols, across all networks and blockchains.

<figure>

![](https://i.imgur.com/gOUhedF.png)

<figcaption align = "center">Figure 1 - Chaincast Overview</figcaption>
</figure>

# 2. Chaincast Protocol Overview

Chaincast is a decentralized protocol that facilitates one-way communication between other decentralized protocols (DAOs) and their stakeholders.

Broadcasts will be immutable. The contents of the broadcast will be stored on a peer-to-peer hypermedia protocol ( IPFS - [https://ipfs.tech/][ipfs] ), a checksum of the message will be produced and saved on the protocol along with its URL.

The broadcasts will be categorized. Different categories will help stakeholders fine-tune exactly the kind of updates they want to receive so as to minimise the noise and superfluous updates. This will allow the stakeholders to chose from which DAOs and which categories in particular they are interested receiving and consuming broadcasts.

In the future, to sustain Chaincast, a fee will be collected for each broadcast. The collected fees will be redistributed to Chaincast's stakeholders according to the tokenomics of Chaincast (CAST) which will be released at a different document and are beyond the scope of this paper.

## 2.1 Broadcast Core Contract

The **BroadcastCore** contract is responsible for the bulk of the Chaincast's on-chain operations. More specifically it:

- Is responsible for registering new DAOs.
- Creates broadcasts.
- Deprecates broadcasts.
- Provides querying functions for broadcast consumption.

The BroadcastCore contract will be upgradeable to facilitate easy and rapid protocol iteration and evolution.

### 2.1.1 Registering New DAOs

To ensure the safety and integrity of the Chaincast protocol as well as the partnering DAOs, the DAO registration will employ a verification process. The goal is to ensure that the people who are requesting to register the DAO, are indeed authorized by the DAO for that action.

Upon registration an address or set of addresses will be added to the allowed list to post broadcasts on behalf of the registering DAO.

### 2.1.2 Broadcasting

Broadcasting, at minimum, will require the following inputs:

- URL to the broadcast message (on IPFS).
- Checkshum SHA256 of the message.
- Category selection.

Broadcast messages are expected to be in [Markdown format][markdown]. While there is no way for a smart-contract to validate this, it is a convention that must be complied with, to promote interoperability and normalization of the distribution systems and consuming clients.

### 2.1.3 Broadcast Deprecation

To account for mistakes or newer updates emerging, a deprecation operation will exist. Deprecation will require:

- Broadcast ID that will get deprecated.
- The new Broadcast ID.

Deprecation will result in the deprecated message to not be visible on normal queries.

### 2.1.4 Broadcasting Categories

Categories define the type of the broadcast, help stakeholders consume the kind of messages they are interested in and allow for custom attributes and behaviours for the broadcasted messages.

Each category will be described by the following properties:

- The ID of the category.
- The name of the category.
- Duration Threshold.

The "Duration Threshold" is expressed in days and provide a rule of thumb to the DAOs as to how often these categories of updates should be broadcasted. They also set expectations to stakeholders as to the frequency and volume of updates they will be receiving.

Chaincast will have the following categories:

|  ID | Name                    | Duration Threshold | Notes                                                                                    |
| --: | ----------------------- | -----------------: | ---------------------------------------------------------------------------------------- |
|   1 | Daily Update            |                  1 | Daily updates for the most engaged stakeholders.                                         |
|   2 | Weekly Update           |                  7 | Weekly updates for the most engaged stakeholders.                                        |
|   3 | Quarterly Update        |                 85 | Quarterly update of the project.                                                         |
|   4 | Vote Needed             |                  7 | A governance vote has been published                                                     |
|   5 | Significant Vote Needed |                 85 | A significant governance vote that warrants big stakeholder participation.               |
|   6 | Security                |                180 | A security breach has happened that requires immediate attention and / or action.        |
|   7 | Action Needed           |                180 | A significant protocol change that requires stakeholder action (a migration or similar). |

Categories are bound to be iterated as feedback and requirements from usage become available.

### 2.1.5 Querying and consuming

Querying for broadcasts is one of the core functions of the Chaincast protocol. As such, querying needs to be versatile and powerful. At the very least, the following criteria will be available to query for broadcasts, alone or in combination:

- DAO IDs.
- Category IDs.
- Offset of records.
- Limit of records.

## 3. Governance

Governance of the Chaincast protocol will happen in a decentralized manner and will dictate all aspects of the protocol. This paper itself is going to be a "living document" residing on a distributed versioning control system (git) and can be amended as per governance decisions.

In particular, the scope of governance include:

- The "Goals and Purpose" of the protocol.
- The Protocol specifications and requirements.
- Amending the Broadcast Categories.
- Amending the Fee Schedule and Base Fees.
- Tokenomics.
- Delegation of decision making power to committees or partners.
- Ratifying agreements with partners for protocol and service maintenance.
- Amending the governance model.

The exact Governance model, processes and procedures will be described in a dedicated Governance Paper.

## 4. Conclusions

The **Chaincast Protocol** helps decentralized protocols inform and alert their stakeholders. It does so in a decentralized, non-custodial manner while allowing end-users to consume the broadcasts in as many ways and through as many media they feel comfortable with.

The core value proposition of the Chaincast protocol is that it allows end users to get the information, updates and alerts they are looking for from one place. As such, it becomes a requirement for the Chaincast Protocol to exist on one network only, serving protocols from all other Layer 1 and Layer 2 networks. Cloning the Chaincast protocol or having multiple instances on alternate networks fundamentaly breaks the value proposition and nullifies the goal and purpose of the protocol.

The Chaincast Protocol aims to be a stepping stone and fundamental block in the proliferation and adoption of Decentralized Protocols.

[markdown]: https://www.markdownguide.org/basic-syntax/
[ipfs]: https://ipfs.tech/
[governance]: #4-governance
