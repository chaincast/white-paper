# Marketing Pitches

## Short description

Chaincast keeps stakeholders informed and up to date by choosing the types and frequency of updates they want to receive from the DAOs they are invested in.

## Long description

Chaincast is a decentralized protocol that facilitates one-way communication between other decentralized protocols (DAOs) and their stakeholders.

Chaincast aggregates, categorizes and normalizes the updates coming out of DAOs so that stakeholders can fine-tune and navigate through the brutal information overload that casually happens when investing on a DAO.

DAOs employ a number of channels and practices to keep in touch with their investors, most common being their announcement channel on their discord server. This is hardly a proper medium for a casual investor to monitor and stay informed as all sorts of announcements are crammed into a single medium. Daily and quarterly updates, important migrations, security updates and all other sort of updates are all jammed on a single communication channel.

Chaincast attempts to solve this problem by providing a structured, normalized platform for all DAOs to publish and broadcast their updates. Stakeholders now have a single place of reference to chose where they get their feeds from. They can select the DAOs they are interested to receive updates from and then can granularly define the frequency of the updates and the type of notifications they want to receive.

For a more technical and details explanation of how Chaincast will work, please visit our White Paper: https://github.com/chaincast/white-paper/blob/main/chaincast-white-paper.md

## How It's Made

Chaincast comprises of various services and platforms:

- Smart Contracts: Is the heart and main state of chaincast, DAOs use the contracts to register and start publishing their updates. Updates are immutable, their content posted on IPFS and the address/hash of that posting is what gets stored on chain.
- Blockchain Indexers: Blockchain Indexers are used to query and fetch the published updates in real-time and distribute them in the backend infrastructure of Chaincast.
- Backend Infrastructure: A fleet of microservices responsible for registering stakeholder preferences and distributing the DAO updates through the multiple channels that will be employed (Push Protocol, email, sms, etc).
- Frontend: Your run of the mill frontend application to tie everything together.

For the purposes of the hackathon, Chaincast will be severely reduced so as to offer a working prototype as a proof of concept.
