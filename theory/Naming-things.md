# Naming things

All of the contestans use some form of hash or encryption key to assign names internally. Similarly as the IP in the current Internet, those are impossible for humans to remember and so all provide some means of mapping human readable names onto those.

In the case of our website publishing system, we will understand those 'names' as "domains". 


## SAFE naming things

SAFE has a very elegant solution to that problem. It's browser defines that the top level domain should be hashed with sha256 and it expect that to be the address of a list of services this name provides. If so, it goes on looking up the service in question. Simple, elegant, easy.

## SWARM names things through Ethereum

Swarm is backed by the Ethereum blockchain global computation cloud. Which, as by itself, is a giant constantly changing state, so for naming things on SWARM you announce it by running a specific "contract" which adds the address to key value list that then any client of the network can look up for you.

While both of these approaches are distributed, the latter is less "decentralised". While in SAFE you'll only know about a specific key once you intend to look it up, in SWARM you have a global directory with all registered names. For example: in the first you can't ever estimate the total successfully, in the later you just count it. This allows for a certain type of simple monitoring as well.

## Naming in Scuttlebot


## Naming with Orbit