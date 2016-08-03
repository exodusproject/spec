# The Exodus Protocol

This document outlines the general design for the Exodus protocol. Technical specifics shall be discussed later, on a different document.

## The Peer-to-Peer Layer

### Resources

The most basic units of the Exodus protocol are _Resources_. These are owned by users, and they represent any piece of data: images, video and audio files, text documents, etc.

### Nodes

Resources are created by, and live in _Nodes_, which generally represent devices running the peer-to-peer software.

### Device Collections and User Identities

A set of nodes owned by the user make up the user's _Collection of Devices_, and these are associated to their _Identity_, which is an abstract representation of the user, and is unique to them (represented in practice by a UUID). In Exodus, we say one peers with other identities, not with devices. Peers exchange Identity information during the initial handshake.

The user may add more devices to their collection via a _Pairing Process_.

### Aggregate Links

Peer relationships between Identities are represented by _Aggregate Links_, which are nothing more than a single logical grouping of multiple connections to a set of devices owned by a user (their Device Collection), with a priority assigned to each device.

Aggregate Links allow us to erase the distinction between devices, effectively enabling the protocol to externally show the collection of devices of User A as a single abstract entity to User B.

### Internal & External Shares

Whenever a user creates a Resource, they have the option of making it either an _Internal Share_ or an _External Share_. Internal Shares are visible only to the user, from any of their devices; and External Shares are visible to any of their peers, regardless of which device originated it, with no apparent distinction.

Read access to External Shares is granted by default to all peers, but peers may request write access to Resources matching certain criteria. This enables features like group collaboration and, as we'll see later, interaction with third-party applications.

## The Distributed Layer

### The DHT

To facilitate peering, DHT capabilities are added to every node, unless a Hub is configured, in which case it takes over an Identity's DHT responsibilities on behalf of every other device in the Device Collection.

Every Identity publishes its UUID along with the address of one device to the DHT, which other Identities can query to obtain up-to-date connection information.

### Local Pairing

_Local Pairing_ is the process through which two Identities in the same geographical vicinity can directly connect with each other, bypassing the DHT.

Local Pairing is made possible by technologies such as Bonjour or NFC.

### Exodus Codes

An _Exodus Code_ is a graphical representation of an Identity's UUID, which can be scanned and decoded by other devices, after which the DHT is queried and the peering process is initiated with the values obtained.

Exodus Codes exist to provide a user-friendly experience for peering.