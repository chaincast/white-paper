# DeFi Broadcast Network White Paper V1

# Abstract

This document describes the DeFi Broadcast Network (DBN - Working title) protocol goals, purpose and functionality.

# 1 Introduction

DBN's goal is to bridge the communication gap between DeFi and all decentralized protocols with their stakeholders. DBN is a one-way, broadcasting protocol that protocols use to broadcast very important updates about them. Stakeholders can then chose from which protocols they want to receive updates and subscribe to these feeds.

DBN is meant to be a very low volume, really high importance update delivery system. The ideal update flow per protocol is considered to be 1 update per quarter. This flow rate will be encouraged through strong disincentives by an ever increasing broadcasting fee, so as to ensure only the most important announcements get through.

DBN is not a governance tool, although it can announce very important governance decisions. DBN can act as an emergency broadcast network, directly informing stakeholders about actions they need to take immediately due to a security breach or other urgent reasons.

The stakeholders will have multiple means of consuming the updates, including directly from on-chain, a website, social media, chat and messaging applications, email, SMS and any other convenient medium.

<figure>

![](https://i.imgur.com/gOUhedF.png)
<figcaption align = "center">Figure 1 - DBN Overview</figcaption>
</figure>

# 2 Protocol Overview

DBN is a decentralized protocol that facilitates one-way communication between other decentralized protocols and their stakeholders.

For each broadcast a fee will be collected and redistributed to the DBN's stakeholders according to the tokenomics of DBN which will be released at a different document and are beyond the scope of this paper.

Broadcasts will be immutable. The contents of the broadcast will be stored on a peer-to-peer hypermedia protocol ( IPFS - https://ipfs.tech/ ), a checksum of the message will be produced and saved on the protocol along with its URL.

The broadcasts will be categorized for finer distribution to interested parties. Different categories will offer varying limits to normal broadcasting fees. For example the "Quarterly Update" category, will allow for 4 base fee broadcasts per year, while the "Emergency" category will only allow 2, beyond those thresholds, the broadcasting fees will increase exponentially.

Stakeholders will have the option to chose from which protocols and which categories in particular they are interested receiving and consuming broadcasts.

## 2.1 Broadcast Core Contract

The **BroadcastCore** contract is responsible for the bulk of the DBN's on-chain operations. More specifically it:

* Is responsible for registering new protocols and the allowed address that can post on their behalf.
* Creates broadcasts.
* Deprecates broadcasts.
* Provides querying functions for broadcast consumption.

The BroadcastCore contract will be upgradeable to facilitate easy and rapid protocol iteration and evolution.

### 2.1.1 Registering New Protocols

To ensure the safety and integrity of the DBN protocol as well as the partnering protocols, the new protocol registration will be a manual process. "Manual" in the sense that it will require a simple but effective verification process. The goal is to ensure that the protocol requesting to register is the official one.

Upon registration an address or set of addresses will be added to the allowed list to post broadcasts on the behalf of the protocol.

### 2.1.2 Broadcasting

Broadcasting will require the following inputs:

* URL to the broadcast message (on IPFS).
* Checkshum SHA256 of the message.
* Category selection.

The broadcasting fee will be collected according to the [Fee Schedule][fee-schedule].

Broadcast messages are expected to be in [Markdown format][markdown]. While there is no way for a smart-contract to validate this, it is a requirement that must be complied with to promote interoperability of the distribution systems.

### 2.1.3 Broadcast Deprecation

To account for mistakes or newer updates emerging, a deprecation operation will exist. Deprecation will require:

* Broadcast ID that will get deprecated.
* The new Broadcast ID.

Deprecation will result in the deprecated message not be visible on normal queries.

Deprecation will collect the base fixed fee.

### 2.1.4 Broadcasting Categories

Categories define the type of the broadcast, help stakeholders consume the kind of messages they are interested in and allow for custom attributes and behaviours for the broadcasting messages.

Each category will be described by the following properties: 

* The ID of the category.
* The name of the category.
* Base fee threshold.

The "Base fee threshold" is expressed in days and determines the time threshold needed for the base fee to apply. More information about how this works and fees are calculated on the [Fee Schedule][fee-schedule].

DBN will start with the following categories:


|  ID | Name          | Base Fee Threshold | Notes                                                                        |
| ---:| ------------- | ------------------:| ---------------------------------------------------------------------------- |
|   1 | Weekly Update        |                 7 | Weekly updates for the most engaged stakeholders.                                                              |
|   2 | Quarterly     |                 85 | Quarterly update of the project.                                             |
|   3 | Emergency     |                180 | An emergency has happened that requires immediate attention and / or action. |
|   4 | Action Needed |                180 | A significant protocol change that requires stakeholder action.              |
|   5 | Vote Needed   |                180 | A significant governance vote that requires stakeholder participation.       |

### 2.1.5 Querying and consuming

Querying for broadcasts is one of the core functions of the DBN protocol. As such, querying needs to be versatile and powerful. The following criteria will be available to query for broadcasts, alone or in combination:

* Protocol IDs.
* Category IDs.
* Limit of records.

## 2.2 Fee Schedule

Fees are the revenue of the protocol and will be used for sustaining DBN and be distributed to DBN stakeholders. Fees will also be used as a deterrent against spamming broadcasts by protocols. This is an important factor so as to both keep the flows low for end-users and also promote the consumption of the broadcasts.

Each broadcast will require 

## 5. Governance

## 6. Conclusions

[fee-schedule]: #2-2-fee-schedule
[markdown]: https://www.markdownguide.org/basic-syntax/
