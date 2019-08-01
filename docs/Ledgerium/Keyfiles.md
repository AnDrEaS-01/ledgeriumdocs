Keyfiles
========

Every account is defined by a pair of keys, a private key and public
key. Accounts are indexed by their *address* which is derived from the
public key by taking the last 20 bytes. Every private key/address pair
is encoded in a *keyfile*. Keyfiles are JSON text files which you can
open and view in any text editor. The critical component of the keyfile,
your account’s private key, is always encrypted, and it is encrypted
with the password you enter when you create the account. Keyfiles are
found in the `keystore` subdirectory of your Ledgerium node’s data
directory. Make sure you backup your keyfiles regularly! See the section
backup-and-restore-accounts for more information.

Creating a key is tantamount to creating an account.

-   You don't need to tell anybody else you're doing it
-   You don't need to synchronize with the blockchain
-   You don't need to run a client
-   You don't even need to be connected to the internet

Of course your new account will not contain any Ether. But it'll be
yours and you can be certain that without your key and your password,
nobody else can ever access it.

It is safe to transfer the entire directory or any individual keyfile
between Ledgerium nodes.

> **warning**
>
> Note that in case you are adding keyfiles to your node from a
> different node, the order of accounts may change. So make sure you do
> not rely or change the index in your scripts or code snippets.
