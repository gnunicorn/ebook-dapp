# The virtual XOR-Address-Space

A key part of any network is how to address things. Like in real life when we want to tell where a parcel is supposed to go, we write an address (usually house number, street and city, maybe country) on to a label to make sure the parcel reaches the right person.

In computer networks we do the same, just that we usually use simple numbers to address something - and we can do that globally. The `IP` (or better `IP-Address`) is such a system. With it we can address a computer at the other end of the world through the TCP protocol. However, the IP address was designed in a certain way so that the TCP protocol could route pakets with the fewest actial hops (a hop is the connection from one computer to the next) and still travel the fastest way across the globe. In order to do that, these are distributed in a certain way that match their physical location.

So, while IP is technically a virtual address space, it is mapped onto the physical world and makes it rather easy to connect traffic to a certain physical locations. Another draw back that comes with it is that it also means we are addressing _one_ specific phyiscal computer. Even though most services don't run in a single location nor on a single computer anymore. However, even when addressing a service like Google or Facebook, we are bound to this physical entry point on some level and it requires complex systems to scale around this limitation.

## Content Hashes

Another way to address something - as mentioned before - could be to use hashes of the content itself. If the hashing function is free from collisions (meaning no two different contents have the same hash ever), this could be a very easy way to address a certain entity without having to know its physical location. One way of thinking of it would be the ISBN of a book. Given a specific ISBN you can walk in any book store of the world and ask for the book of that ISBN and if they happen to have a copy, you can fetch it. You don't have to address the book in the same way as we had to do for the parcel before.

Now, if you think of hashes, like SHA256 (the most commonly used among our contestants), the you probably know it in a hex-format like this `c9f933d8d449c3c9c4618ce8d9d9b438cb1abe11b940f072f73252bf7df9bb06`, which is just a base-16 format of a very big number (`91355185319135079095732316493494045725379585213541497236226218904791000136454` in base 10, or `1100100111111001001100111101100011010100010010011100001111001001110001000110000110001100111010001101100111011001101101000011100011001011000110101011111000010001101110010100000011110000011100101111011100110010010100101011111101111101111110011011101100000110` in binary). However, given a magnet-link with this address, your a Bittorrent client might be able to fetch you that content (saying "hello reader") and through hashing the content you can easily verify its autheniticity.

## Distributed Hash Tables (DHT)

But how would a Bittorrent client known which other clients to ask for the content. After all you don't want to have to go into every shop in the world to ask for the book with a specific ISBN either. Well, a simple way would be to keep a large register of all the content-addresses and which clients offer it. Which is sort-of what 'trackers' in the bittorrent eco-system do. However, that means you are back at a somewhat centralised system and considering how incredibly huge this list would be, we can't expect every client to hold it.

This is where the idea of Distributed Hash Tables, and specifically the Kadmelia implementation of, comes in. As the name suggests instead of holding one giant list (hash table), we distribute it on the network. And we assign responsibility for holding certain sub-set parts of the list within the network through a rather simple mechanism: proximity.

### XOR Distance

In order to join a Kadmelia Network the client must assign itself a random number in the same address-space as the content addresses. So in case of our SHA256-example, we could just create a random string at startup, hash it and call that our `Id`. If that `Id` already exists, the connection is rejected and we try again with another random `Id`.

Now, when we join, the partie we connect to let us know of other parties that are `close` to us, that they know of. While in reality we'll use XOR-Distance (because that is really cheap to calculate for a computer, while harder to predict from the outside), you can think of substracing your id from the id of the other party, giving you a unique distance to any other party in the network. Now, any client can easily figure out which are their closest (virtual) neighboors. Because that happens with the XOR-Opperation, this is often referred to as the XOR-Namespace or XOR-Network.

As the content-addresses are in the same number space, we can calculate that same distance between any client id and content address. Thus have a simple but very powerful way to determine, who's responsible for knowing about this particular entry: who ever is closest to it (or maybe the 3-4 that are closest, depending on the actual implementation)

### Kadmelia routing

However, in order to know whether any other is closer than us to that particular address, we need to know about our closest neighboors though. So, when we are told about them, we'll hold a static connection to them to ensure they are still there. And if they drop out we might have to take over responsibility. While at the same time, we'll hold much fewer connections to the more distant parts of the network (from our perspective). And we'll try to keep them evenly distributed. So whenever a client connects to us with a connection that leads to a more distributed address space for us, we might drop other connections.

With this set of maybe 10-15 connections (5 to our closest neighboors, 5 in the next closest circle and a few more far out in space from our point of view) we can now easily respond to any query of of the DHT, look up as well as storage: Whenever a request comes in we calculate the distance to the object in question and figure out whether we are responsible, in which case we check our part of the table, or send the request further to the next closest entity we know of.

As this entity also holds the connections to their closest neighboors it takes only very few hops in order to reach the entity responsible for a certain address.

#### In Bittorrent

In bittorrent this mechanism is used to assign the responsibility of all parts of that distributed hash table to clients. However, the value of each entry still is just a list of IP-addresses (with port-information) of clients that have been announced before that they had that content and that information is then sent back for the client to connect to them. Thus bittorrent itself relies on physical addressing, it just uses this system for lookup.

#### Forwarding Kadmelia

However, the system is just a way to assign responsibility and it doesn't have to point to IPs in general. Quite the opposite, you could use (and that is what our contestants do) that system to define, which client might be responsible to hold a specifc piece of data. And then, use that same routing mechanism to respond to that request: by sending the data back to, whoever hop asked you about it.

In this system, you can be able to address any content in the world by just asking the closest neighboor you know should be responsible and they will ask whoever is closer and so on but you'd simply hear back from that closet neighboor only. Thus no one would actually know, who requested nor, who really provided that information - as no hop (aside from the two at either end) knows where in the route they were.

This system is often referred to as Forwarding Kadmelia as it is based on kadmelia but used to forward the actual content rather than just the reference to that content.

## XOR Consensus

But you could use that XOR-Namespace for more than just assigning data holding responsibility. As we've hinted to before, you could make any number of responsibilities out based on this simple mechanism: like verifying information (for e.g. a correct signature) or provide a consensus mechanism. Especially if they are based on the closeness, then they are quite fast as the clients are already holding the connection to the other parties.

### vs. Blockchain

As discussed in the previous chapter, in order to find consensus blockchain usually use an elaborate electable-reduction-system that everyone - eventually - votes and agrees upon. And as that is based on blocks, everyone sort-of needs know of and have access to all blocks: this doesn't scale very well, one of the main critizisms on blockchain technology in general (the other being speed of finding actual consensus). In this XOR-Consensus, rather than reducing the electables, we reduce the electors and ensure that tempering with is out of the question because you are randomly assigned and you better play by the rules or your neighboors will cut you out.