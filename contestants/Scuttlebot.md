# Secure Scuttlebot

Unlike any other, [Secure Scuttlebot](https://scuttlebot.io) is built with social networks in mind, which gives it some interesting properties. From the ground up, Secure Scuttlebot is an append-only log, similar to a blockchain but that every participant has their own and only they are able to add messages to it. So, while anyone might replicate any log, only the owner would be able to add new messages.

Thus, it is just natural to understad that as a social network participants own "news feed". And in order to "combine" the news feeds of ones network, one must simply go through all the ones one follows and read their streams. That's exactly what "Secure Scuttlebot" does, whenever you fire it up. And as any other peer-to-peer it can use a range of connections to read the data from - while encryption makes sure that a log may only contain valid entries added by the owner. So, you don't have to trust any party in the system giving you data, similar as in IPFS the client can verify itself that the data is valid.

Another interesting property that is given through that system is, that unlike most blockchains, you don't need to replicate a global state, you'd only replicate the state of your social network - currently defined as friends and your friends friends. And through that an entity popular enough can also be reasonably sure to be kept online even when turning off their computer.

Which also brings us to a weakness though, that I am not able to find a particular answer to: what if the owner created a fork? Within that system it would theoretically be possible that the owner tells a certain part of the network, that a certain item has been appended while it tells another parts that a different part has been appended. 

Secure Scuttlebot has some excellent high level documentation, I must say. It answers many questions clearly and in an easy language. Among others it describes the message protocol (of an entry in the 'feeds blockchain') and how it can even be used for secure end-to-end-encryption. Same as the others, Secure Scuttlebot comes with a public-key infrastructure built-in.

While it has clearly been designed for the social network use-case, and impressivly so, I might add, the system allows all sorts of decentributed apps as well. The project website lists six, though all largely related to the social network use case. The most impressive one of them is a fully decentributed github-style code publishing and project management system that even comes with its own git-extension for direct uploads.

We'll take a closer look at the functionality and how to model all types of software with this elegantly simple system when we try to build apps with it.