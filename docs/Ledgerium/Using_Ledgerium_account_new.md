Using `ledgerium account new`
=============================

Once you have the ledgerium client installed, creating an account is
merely a case of executing the `ledgerium account new` command in a
terminal.

Note that you do not have to run the ledgerium client or sync up with
the blockchain to use the `ledgerium account` command.

``` {.sourceCode .bash}
$ ledgerium account new

  Your new account is locked with a password. Please give a password. Do not forget this password.
  Passphrase:
  Repeat Passphrase:
  Address: {168bc315a2ee09042d83d7c5811b533620531f67}
```

For non-interactive use you supply a plaintext password file as argument
to the `--password` flag. The data in the file consists of the raw bytes
of the password optionally followed by a single newline.

``` {.sourceCode .bash}
$ ledgerium --password /path/to/password account new
```

> **warning**
>
> The `--password` flag is meant to be used only for testing or
> automation in trusted environments. It is a bad idea to save your
> password to file or expose it in any other way. If you do use the
> `--password` flag with a password file, make sure the file is not
> readable or even listable for anyone but you. You can achieve this in
> Mac/Linux systems with:

``` {.sourceCode .bash}
touch /path/to/password
chmod 600 /path/to/password
cat > /path/to/password
>I type my pass
```

To list all the accounts with keyfiles currently in your `keystore`
folder use the `list` subcommand of the `ledgerium account` command:

``` {.sourceCode .bash}
$ ledgerium account list

account #0: {a94f5374fce5edbc8e2a8697c15331677e6ebf0b}
account #1: {c385233b188811c9f355d4caec14df86d6248235}
account #2: {7f444580bfef4b9bc7e14eb7fb2a029336b07c9d}
```

The filenames of keyfiles has the format
`UTC--<created_at UTC ISO8601>-<address hex>`. The order of accounts
when listing, is lexicographic, but as a consequence of the timestamp
format, it is actually order of creation.
