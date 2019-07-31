Importing an unencrypted private key
====================================

Importing an unencrypted private key is supported by `geth`

``` {.sourceCode .bash}
geth account import /path/to/<keyfile>
```

This command imports an unencrypted private key from the plain text file
`<keyfile>` and creates a new account and prints the address. The
keyfile is assumed to contain an unencrypted private key as canonical EC
raw bytes encoded into hex. The account is saved in encrypted format,
you are prompted for a passphrase. You must remember this passphrase to
unlock your account in the future.

An example where the data directory is specified. If the `--datadir`
flag is not used, the new account will be created in the default data
directory, i.e., the keyfile will be placed in the `keystore`
subdirectory of the data directory.

``` {.sourceCode .bash}
$ geth --datadir /someOtherEthDataDir  account import ./key.prv
The new account will be encrypted with a passphrase.
Please enter a passphrase now.
Passphrase:
Repeat Passphrase:
Address: {7f444580bfef4b9bc7e14eb7fb2a029336b07c9d}
```

For non-interactive use the passphrase can be specified with the
`--password` flag:

``` {.sourceCode .bash}
geth --password <passwordfile> account import <keyfile>
```

> **note**
>
> Since you can directly copy your encrypted accounts to another
> Ethereum instance, this import/export mechanism is not needed when you
> transfer an account between nodes.

> **warning**
>
> When you copy keys into an existing node's `keystore`, the order of
> accounts you are used to may change. Therefore you make sure you
> either do not rely on the account order or double-check and update the
> indexes used in your scripts.
