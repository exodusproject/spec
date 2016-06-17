The protocol could listen on two ports: the protocol port and the data port

The protocol port would be used for administrative tasks and peer interaction not directly involving data itself. Messages exchanged through the protocol port could be defined to be in a wire format, much like DNS messages, with a similar compression algorithm. This would make the protocol speedy and very lightweight (at the cost of complexity for us)

Data exchanged through the data port could use a more human-friendly format, such as JSON, or a series of \r\n terminated lines (which has been working for everything else on the internet for years)

The network is a meshnet. Each server is a peer, with an internal routing cache. When first joining the net, a server peers with another but doesn't download the entire table.

When wanting to get a message or subscribing to another server, your server queries one of its peers to check if that server exists within its routing table. If it doesn't, a "resolving chain" process occurs, exactly as in DNS, until a server capable of resolving the route is found, in which moment your server adds the server it wanted to subscribe to as a peer.

Servers can declare themselves as non-peering to avoid excessive peering and avoid routing ambiguity, and to allow for "hub" designs where several smaller servers only add a larger server to their peer list, then making this larger server effectively act as a DNS cache server.