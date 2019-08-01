Using Ledgerium console
=======================

In order to create a new account using ledgerium, we must first start
ledgerium in console mode (or you can use `ledgerium attach` to attach a
console to an already running instance):

``` {.sourceCode .bash}
> ledgerium console 2>> file_to_log_output
instance: ledgerium/v1.4.0-unstable/linux/go1.5.1
coinbase: coinbase: [object Object]
at block: 865174 (Mon, 18 Jan 2016 02:58:53 GMT)
datadir: /home/USERNAME/.ledgerium
```

The console allows you to interact with your local node by issuing
commands. For example, try the command to list your accounts:

``` {.sourceCode .javascript}
> eth.accounts

{
code: -32000,
message: "no keys in store"
}
```

This shows that you have no accounts. You can also create an account
from the console:

``` {.sourceCode .javascript}
> personal.newAccount()
Passphrase:
Repeat passphrase:
"0xb2f69ddf70297958e582a0cc98bce43294f1007d"
```

> **note**
>
> Remember to use a strong and randomly generated password.

We just created our first account. If we try to list our accounts again
we can see our new account:

``` {.sourceCode .javascript}
> eth.accounts
["0xb2f69ddf70297958e582a0cc98bce43294f1007d"]
```
