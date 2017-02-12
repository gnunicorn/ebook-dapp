# the SAFE Network

Developed by MaidSafe Ltd for over ten years now, SAFE has been in the works the longest. However within that time frame it has been rewritten two times, thus the current code base in Rust is less than three years old. 

SAFE is using the previously mentioned Xor-Virtual-Address-Space and takes it to excellance. All its internal logic is based on that system, including to manage multi-step transactional process: the full-featured nodes - called Vaults - must be capable to take over any supported Routing Persona, a role in any process, at any given time and will be cross-checked to follow it by its closest neighboors. 

Through this model, SAFE implements a range of different Data-Types, which have their own processes in the sytem. For example a specific Data-Type and Process to allow for registration and authentication against the network without any third party. Or the immutable-data which is defined as having to be stored under its hashes content address. A simple but network confirmed process. There used to be multiple mutable data types, which are currently condensed into a general-purpose key-value-store-style MutableData-Object. 

## privacy-first

One very interesting aspect about SAFE lies in its founding story: lead by the terrible privacy attributes of the current internet, the founder set out to develope a system that completely removes the "central"-server from the equation. These two key morals, privacy and decentribution, shine through the product in many angles. For example, by default, all data leaving a clients computer is encrypted: either with their private key, a shared key or anothers public key - but even "public" Data.

Through a process called self-encryption SAFE splits any piece of unencrypted data into a bunch of chunks which are then used to encrypt one another and which can only be decrypted knowing their order. This order is then stored in a so called "data map", which allows you to decrypt all these chunks, while you can be fine with storing them on random persons computer: each chunk is just junk and totally useless. Which also means any file is actually distributed in the network, too.

One great feature of this process is that is allows for resonable security, while also allow for de-multiplication: anyone, who already has the file can easily calculate that data map, which is always the same for the same file. And when they want to store that data in the network, the network already has the data in store. Yet, you still need that data map and by sending this encrypted on the network only, you can assume reasonable security of the data stored. Meaning the network can perform much better and data is only stored once - rather than as often as might want to share it with someone.

Secondly, this has two great features from a general systems perspective: a) I, running a vault, can plausibly deny to have "serve" any illegal content as I have no way of knowing if that chunk might be part of any such file, b) if you only encrypt the sensitive information, it is easy to identify what is important and should be attacked, but if everything stored on any system is just utter junk, your data is much safer, as it is even hard to identify in the first place.

