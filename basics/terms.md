# Terminology

Before we can talk about and how to structure and build DApps, we first have to define a few terms, first and foremost what actually consistutes as an DApp.

## Decentral vs Distributed vs Decentributed

Depending on who you ask, the "D" in DApp stands for Decentralized or Distributed Application. And while the distinction between the two matter, for the purpose of this book we'll take a very narrow definition in which we can and will use the terms interchangably.

By itself decentralisation is really just expressing that there is no central authority or single point of failure, something that distribution kinda of implies. However, also any federated network is a decentralised one and that is not what we mean in this context. In a federated system you'd have many servers that clients interact with and that then interact between one another. A good example of a federated application is email or the XMMP jabber service. However, in its traditional usage, the word "distributed" also doesn't entirely express what we are talking about: it comes from control networks, like distributing information accross a controlled database cluster through sharding. In most of these scenarios, while the data might be "distributed" it is usually still under the control of one organisation. For example, Gmail's backend is distributed.  

For the purpose of this book, neither of them are considered DApps. In this book we are talking about **public peer-to-peer-networks**, that everyone can join, participate in and with the, more or less, equal powers and responsibilities as any other party. Because of these historic usage of these words many feel that neither "decentral" nor "distributed" really capture the nature of the apps we want to talk about. This is often made visible through using the `Đ` or words like distributilized or decentributed. For the purpose of this book we'll use these interchangably, all meaning this very narrow definition.



## Infrastructure / Platform / System

All of our contestants provide a new virtual network ontop of the TCP/IP protocol, but because they often include various features of the higher level, it isn't applicable to think of them as just protocols in the stack. Most of them are designed with modern app development in mind and provide features like authentication and privacy that otherwise apps have to implement themselves. As such, when thinking of our contestants, we'll refer to them as infrastructure, system or platforms and we'll use these names interchangably as none appears to be more apt than the others.
