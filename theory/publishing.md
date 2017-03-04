# The theory of publishing

## XOR-Namespace

Within the XOR-Namespace, that publishing and updating content is quite simple. For the developer these systems act as a giant, global key=value store and both SWARM and SAFE provide an authentication system after which a participant can choose any random key they want to publish something under and "put" their content onto the network behind that key.

Both system also provide some means to authenticate, who or what can mutate the given entity after. SAFE is a bit further in that regard, as the system itself can distinguish between different types of data behind such a key and depending on those, the network itself may or may not allow certain operations or interact with or upon the data differently. In the case of SWARM we are, as of today, mostly bound to being able to mutate data through replacing it with a cryptographically signed request.

So in order to publish something, we just generate a random key or based on an external source and store our data there. Then we need to share that address with whomever we want to be able to contact that, too - or the way they can calculate said address.

## Immutable Logs

This way of addressing doesn't work in immutable systems, where the address is strongly bound to its content. Thus, whenever the content is updates it actually creates a new address - hence the name "content addressing". This is true for blockchains as well as for the bittorrent-like IPFS system. Publishing in these systems is very easy: you just create the content and announce to the network that you have a copy of it.

But how do you "mutate"? Well, you can't, not that specific piece of content. Instead what you do is create a linked chain of content and always announce the "latest one" to the network. Within each entry you keep a reference to the previous one - the basics of a blockchain - and in each entry you don't keep the actual state but instead a state transition (or "transaction"): the change that happened from the previous state. In order to figure out the current state a computer now just fetches the entire chain all the way to when it last knew about it and recreates the current state by applying those changes in order.

In the case of Secure Scuttlebot this is build into the system itself: every participant has their own signed blockchain of an "activity feed" that only they can write to. And whenever an update is made, that is announced to the network and they update their latest reference. As the owner has to sign that request, it is very easy for any node to confirm that it was the owner who said this is the new latest state and fetch the updates.

IPFS itself doesn't know about such a system, but Orbit implements essentially the same on top. However, for "announcing" it uses a more experimental feature of publish subscribe that isn't activated on all clients at the moment. But internally it uses IPLD (InterPlantary Linked Data) which is the only format specified so far that has the capability to link outside of its own network.

## Benefits and drawbacks

From reading these two paragraphs one things should have become immediately clear: the earlier provides something closer to a state-changing database while the later is more of a ledger or transaction record. With the ups and downs these systems bring: while the database scales quite well, you have little record of understanding how you got the current state and have to "blindly trust" that it arrived there correctly. While the continuous log provides that feature, including finding and fixing bugs recorded in the past, a contentiously growing log is not scaling very well. Some attempts of providing "snapshots" are being experimented with in many blockchain technologies in order to fix that problem.

The immutable logs as provided here come with another interesting features though: history rewriting and offline capability. As you are muting your very own block you can do that locally and push one or many updates at any point later. Though this isn't specifically implemented at the moment, by itself it is much easier to come to the current state with a CRDT system that can queue changes and apply them later, than if you always need to be connected to change things.

Secondly, though you are providing the history through links, you can also rewrite it in the same way as git allows you to do it. By going back in time one item before the one you want to change, you can create a complete new chain of changes from that point and announce the latest one as the new current state. As you are its owner, that is a completely valid activity. Sure someone might still keep the old data around, but you just told everyone that something else is the latest current state and they are trusting you as the owner.

Scuttlebot and IPFS face the fire-and-forget problem though. By having to be connected and ensuring data retention once data has been uploaded in SWARM and SAFE you can switch off your system and the data will be available from any other system. Scuttlebot and IPFS do not give any such guarantee. Quite the opposite within IPFS's Orbit you always need at least one instance of your app running because the "latest block" is hold only on those clients but not store on the network itself. Should you be firing that signal while no other client listens and switch your computer off, the update might simply hasn't happened. It is also a bit unclear how the system reacts or is supposed to be action on a netsplit and competing "latest states".

Scuttlebot has an very interesting approach to that problem: by basing their entire infrastructure on the "social graph" any client that you follow or anyone they follow (the social network of two degrees) and keep that state continuously updated. Thus, so goes the argument, any of your blockchain will instantaneously be updated by a range of your friends and friends' friends - a circle big enough to assume that there is always a client up and running. While facebooks activity numbers would support this claim, it has to show whether that stacks up in reality - especially in the beginning while the network is still small.

