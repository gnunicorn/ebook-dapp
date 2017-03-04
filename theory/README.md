# Theory

To recap, we are going to look at two competing models for the distributed web. On one side we have the "always on global p2p network" that SAFE and SWARM intend to provide, using the XOR-Virtual-Namespace and predicatible randomness to ensure consistency. On the side we are looking at continous immutable logs, implemented in Secure Scuttlebot in the form of a range of distributed blockchains and in IPFS's Orbit with immutable pointers that are announced through PubSub.

These are the two main competing models to solve the issue of decentribution today. As you might notice, the super hyped "blockchain" implementation is only one among four that are looking at (though Swarm is closely alligned with the Ethereum Blockchain). Most blockchain technology by itself doesn't actually solve the problems we are specifically looking at.

Before we go into the depth of building and publishing our first apps on these networks, we want to compare these two competing models and understand their general approach on what we are about to do next: what happens under the hood?