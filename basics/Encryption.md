# Encryption

A lot, if not all, in peer-to-peer systems stands and falls with encryption. In a system where you can't trust information based on the party that supplies it (like the 'server') authority and authenticity must be proven in different ways. Math has been found to be a rather great way to proof correctness (and other attributes) of things and that is what encryption means in this context: some cool Math. And even though you don't need to understand all the cryptographic algorithms used, you need to understand some basic properties of the various types of crypto that is used in order to follow what is going on.

## Hashing

If you are familiar with downloading files from the internet or using bittorrent, you probably know already about hashes. In encryption hashing describes a function that given a specific input, gives you a determined output, while it is very hard to make the reverse: given a determined output it is really hard to figure out what that input might have been. Usually the hash (it's result) is also much smaller than the input 

Especially when a hash function guarantees uniqueness - will give you a unique ouput for every single input - this can be used to proof that something is the same as before. For example, given the hash of a content of a file you can easily calculate and check it against a given hash to ensure that the content hasn't been tampered with. This is what md5checksum are intended to provide.

As these hashes are unique, they can also be used to _address_ an object by its content. That is what magnet-links in bittorrent are doing. Rather than saying you want a file located here or there, you say, you want the file with the content for which that hash is appropriate. This is called content-addressing and plays a vital role in peer-to-peer systems.

## Symmetric Encryption

Similarly you are probably familiar with symmetric encryption and have used it at least once before when you used a password to decrypt some information. Symmetric Encryption is when you use the same password to en- and decrypt an information. It's one of the most obvious ways to encrypt something and the easiest to understand. And very applicable if we want to encrypt something that only those with access to that same secret can decrypt. However, it comes with the drawback, that there is no way to prevent someone to use that password to encrypt something themselves.

## Asymmetric Encryption

Other with asymmetric encryption, where there are two keys one to encrypt something and another to decrypt. While this sounds counter intuitive at first, this has a variety of usages. For example could you only share the encryption key with someone else and the decryption key with no one else. That would allow the other party to create messages that only you could decipher (decrypt).

This is especially handy if the key-pair works both ways: this way you could publish a public key that anyone could use to encrypt a message to you or verify that a message has actually come from you, because you are the only party having access to the other key. In this type of system we refer to them as private (secret) and public keys. 

### Signatures

You can also use this feature of asymmetric encryption to verify that a request has been by an entity with access to a specific secret by using their public key to decrypt the message and find a certain expected outcome. This is similar as hashing (as the hash is usually signed) but can verify source.

### Public-Key-Infrastucture

This is only useful if there is a way to know about the public part of these key-paris. The way we discover and known of these is called a "public-key infrastructure". After all we can't reliably verify a signature if we don't know which public key to use to verify it with. A public key infrastructure provides a way for use to retrieve the appropriate key we need for verification.

