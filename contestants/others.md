## Other Platforms

With a specifc focus of being able to build web-based apps ontop of the platform, we've selected the given said of platforms as primary targets to do the tests on. That said, there are others we'd like to have briefly discussed and mentioned why they aren't included (at this point in time).

### [Enigma](https://www.enigma.co/)

Enigma is very interesting project, that promises privacy-first distributed computation. They achieve this with an off-blockchain network that uses the same kadmelia routing system to compute designate responsibility. However, other than many existing platforms, the Enigma system provides a strict distinction between public and private information and computation and ensure the later only happens in chunks that are useless and don't leak any information onto the system they are run on.

While the system is very interesting and highly promising, Enigma has only been described in a Whitepaper yet and as such still misses any publicly known implementation of it. Hence the reason we did not include it. 

### [Tahoe-LAFS](https://tahoe-lafs.org/trac/tahoe-lafs)

Tahoe LAFS is a long-term running, operational and very interesting idea. In its core it consists of two parts: client-side encryption of all data and redundant storage. The project has been around for over a decade and offers their service successfully for quite a while. However, for the purpose of this DApp idea, it is still a client-server-model that is neither actually distributed nor peer-to-peer. If you are a looking for a secure back-up in the cloud, however, this might be a very good choice!

### [ZeroNet](https://zeronet.io/)

With its clear focus on offering a new data distribution model for the current web, ZeroNot is right at the heart of what we are discussing. And it does offer some interesting ideas and features by combinging "bitcoin crypto" with bittorrent. Primarily the feature that by accessing a site, you also become a host of the same and thus very popular sites will spread widely and are accessible easily - a bittorrent classic. However, this comes with the significant drawback of leaking privacy relevant information: as this requires your IP to get the data, it is rather easy to track which web-sites you are accessing. For privacy, ZeroNet advocates to use the Tor-Network, which - but that is just a a guess from the author - would probably destroy all those speed ups you've just gotten from the bittorrent protocol.

Further more, as it is modelled after bittorrent and doesn't offer any inherent incentives, there is no guarantee for any website to stay alive after the last person accessed them. Though, while the system claims to be "build for dynamic websites", it gives no guanrantees that data will stay available once you close your instance of it.

### [Storj](https://storj.io/)

StorJ is another recent addition to the world of decentralized network service. It's main focus is to create a competition to for cloud storage services like Dropbox or Amazon that is using peer-to-peer storage instead. It, too, has an incentive system that allows you to "rent out" your own storage to the network and have others pay for using it. And while it is also using many of the underlying technologies as the other frameworks, as it specializes on (file-based) data storage, it doesn't really allow DApps: as of today it has no way to publish or browse public content or apps - everything is encrypted with the users credentials. Making it unapplicable for our use cases.

### [Freenet](https://freenetproject.org/)

Freenet is another project that has been around for a while (since the early 2000th actually) and seen significant adoption and usage over the years. Started long before bittorrent and the distributed hash-table was first descripbed it uses its own mechanism to distribute data accross a peer-to-peer network of untrusted nodes. While it offers some data redundancy and retention it doesn't guarantee these - quite the opposite: because of the way that data is allocated and retrieved, by design, the network "forgets" about data that hasn't been requested in a while. Though some consider this a feature, from the perspective of a developer, this is terrible: my backend (/database) has one job and that is to keep the data around and accessible. It should never loose it. Though this is pure speculation, maybe that is one of the reasons why this system never saw wide spread adoption although being around for such a long time.

### [IPDB](https://ipdb.foundation/) with [BigchainDB](https://www.bigchaindb.com/)

The InterPlanetary DataBase projects understands itself as the complementary Database to the IPFS file storage solution. Based on, and pushed by the people behind, BigchainDB it is not, as the name suggest, a blockchain-based technology but rather the idea of merging the features of blockchains and high scaling databases. At the writing BigchainDB is an extension to the MongoDB-Database which acts in an append-only-based block-wise-fashion (as we know from blockchains) and within a federated consesus of other trusted databases.

The idea behind IPDB is to provide this as a trusted service run by a multi-nationally run federated network of members of the foundation behind the system. It intends to provide trust mainly through having too many parties, each one of them trusted, too agree for an attack - and the statues of the foundation reflect that (by for e.g. insisting that the majority must always be hold by non-profit entities). The reason we did not include it in our list, is two parts: for one it isn't available to the public yet, so we can't. But secondly, and more importantly, it is federated - which we do not consider fully decentributed in our scheme of things.