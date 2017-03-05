# Naming things

All of the contestans use some form of hash or encryption key to assign names internally. Similarly as the IP in the current Internet, those are impossible for humans to remember and so all provide some means of mapping human readable names onto those.

In the case of our website publishing system, we will understand those 'names' as "domains". 


## SAFE naming things

SAFE has a very elegant solution to that problem. It's browser defines that the top level domain should be hashed with sha256 and it expect that to be the address of a list of services this name provides. If so, it goes on looking up the service in question. Simple, elegant, easy.

## SWARM names things through Ethereum

Swarm is backed by the Ethereum blockchain global computation cloud. Which, as by itself, is a giant constantly changing state, so for naming things on SWARM you announce it by running a specific "contract" which adds the address to key value list that then any client of the network can look up for you.

While both of these approaches are distributed, the latter is less "decentralised". While in SAFE you'll only know about a specific key once you intend to look it up, in SWARM you have a global directory with all registered names. For example: in the first you can't ever estimate the total successfully, in the later you just count it. This allows for a certain type of simple monitoring as well.

## Naming in Scuttlebot

Scuttlebot, too, defers the actual implementation of a naming system into the implementation layer on top of, but it provides an interesting distribution mechanism. Their DNS-system acts very much like a class DNS-server, down to the format of each individual record but unlike the classical hierarchy it build this list out of the individual records that your social graph has published and therefore "vouched" for. So rather than having one "global state" you'd always have a local state that is different for each client because of their social circle. Such a system is often referred to as a pet-name infrastructure, because anyone can name their pets as they please.

That means that in order to globally be "understood as something" you need to convince a lot of people about calling you that way. But any individual could still decide to publish it under a different name. So in one circle you might find the website under the name "Facebook" while in others, you'd find the same under "GesichtsBuch" or even "FakeNews".

Interestingly this system, some argue, is closer to how we function as humans in populations. Within differrent social circles, we have different names for the same things and within these circles there is a common understand (through usage) about them. And things that are popular, will, naturally become know under the same name to a wider audience over time.

So in order to publish our website, we'd have to name it and have a social circles that is willing to replicate/accept the name we gave it and refer to it as such, too. Therefore, before the act of publishing and naming, I have to build up a circle of people, who trust me and replicate my names or I simply won't get far with it. A highly interesting anti-spam mechanism.

## Naming with IPFS/Orbit

IPFS has for long struggled with providing a common naming mechanism, and up to this day doesn't provide any in of itself. It's default tool allows to run in proxy-mode which serves up any ipfs-url directly and such the whole hex-encoded is often shared. Many actually consider that a benefit as those address can never change, so you can trust them, the argument goes. But in the same way that those are inaccessible to normal humans as bitcoin addresses are, this argument hasn't cought on with the masses.

So IPFS overall went a different approach of "enhancing the web": rather than providing its own browser and naming system, IPFS is available as an in-browser-library. So you can just host a random website somewhere and use the library to fire up an IPFS client that then loads the actual content of the website. And if you want it to serve a new version, you just replace the link in that website. While this means, you can easily use IPFS today as a CDN without any requirements on the user, it also means you are still stuck on our centralised infrastructure.

And as you might have noticed, Orbit is an external service _using_ IPFS as a node-process. So this model of loading it in the browser isn't applicable here, but instead the user must run the IPFS-proxy as well as the Orbit-Server on some system (owned or trusted). Would they come bundled in some browser, this might force people to think about an independent naming system - but we aren't there and it is unclear if the community ever wants to go into that direction at all.

Within Orbit, a "feed" is named globally at setup. Meaning two feeds with the name are considered of the same origin. It therefore does have the general key-value-store-idea we discussed earlier. But unlike those previous systems, anyone can claim any name and there is no varification that you might be trying to take over an existing one. Which is fine enough for our first case of having anyone publish comments on a blog post, but it is obvious that this will cause trouble whenever we need more trusted ways of mutating content.