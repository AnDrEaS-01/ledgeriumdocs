Solidity
========

Solidity is an object-oriented, high-level language for implementing
smart contracts. Smart contracts are programs which govern the behaviour
of accounts within the Ethereum state.

Solidity was influenced by C++, Python and JavaScript and is designed to
target the Ethereum Virtual Machine (EVM).

Solidity is statically typed, supports inheritance, libraries and
complex user-defined types among other features.

With Solidity you can create contracts for uses such as voting,
crowdfunding, blind auctions, and multi-signature wallets.

When deploying contracts, you should use the latest released version of
Solidity. This is because breaking changes as well as new features and
bug fixes are introduced regularly. We currently use a 0.x version
number to indicate this fast pace of change.

## **Solidity**  
Solidity is a high level smart contract language similar to JavaScript which allows you to develop contracts and compile to EVM bytecode. It is currently the flagship language of Ethereum and the most popular. Smart Contracts are compiled using the solidity compiler and turn into Etheruem binary format called bytecode which are deployed to the blockchain. This bytecode gets executed by the Ethereum Virtual Machine (EVM).

-   [Solidity Documentation](http://solidity.readthedocs.org/en/latest/) - Solidity is the flagship Ledgerium high level language that is used to write contracts.
-   [The ReMix IDE](https://remix.ethereum.org/)
-   [Standardized Sample Contracts](https://github.com/OpenZeppelin/openzeppelin-contracts)
-   [Useful Ðapp Patterns](https://github.com/Ledgerium/wiki/wiki/Useful-Ðapp-Patterns)

## **Writing a contract**
A "Hello World" program in Solidity is of even less use than in other languages, but still:
```
pragma solidity ^0.5.1;

contract HelloWorld {
  function helloWorld() external pure returns (string memory) {
    return "Hello, World!";
  }
}
```
This contract will send greet message after its construction.

## **Compiling a contract**
Compilation of solidity contracts can be accomplished via a number of mechanisms.

-   Using the `solc` compiler via the command line.
-   Using `web3.eth.compile.solidity` in the javascript console
    provided by `geth` or `eth` (This still requires the `solc`
    compiler to be installed).
-   The [online Solidity realtime
    compiler](https://Ledgerium.github.io/browser-solidity/).
-   The [ReMix IDE](https://remix.ethereum.org/).
-   The [Ethereum Wallet](https://github.com/Ethereum/mist/releases).

**Note**  
More information on solc and compiling Solidity contract code can be found [here](https://solidity.readthedocs.io/en/v0.5.10/using-the-compiler.html).

### Compiling a simple contract


### **Create and deploy a contract**

Before you begin this section, make sure you have both an unlocked
account as well as some funds.

You will now create a contract on the blockchain by [sending a
transaction](https://github.com/Ledgerium/wiki/wiki/JavaScript-API#web3ethsendtransaction)
to the empty address with the EVM code from the previous section as
data.

**note**

This can be accomplished much easier using the [online Solidity
realtime compiler](https://Ledgerium.github.io/browser-solidity/) or
the [Mix
IDE](https://github.com/Ledgerium/wiki/wiki/Mix:-The-DApp-IDE)
program.

``` {.sourceCode .js}
var primaryAddress = eth.accounts[0]
var abi = [{ constant: false, inputs: { name: 'a', type: 'uint256' } }]
var MyContract = eth.contract(abi)
var contract = MyContract.new(arg1, arg2, ..., {from: primaryAddress, data: EVMByteCodeFromPreviousSection})
```

All binary data is serialised in hexadecimal form. Hex strings always
have a hex prefix `0x`.

**note**

Note that `arg1, arg2, ...` are the arguments for the contract
:   constructor, in case it accepts any. If the contract does not
    require any constructor arguments then these arguments can be
    omitted.

It is worth pointing out that this step requires you to pay for
execution. Your balance on the account (that you put as sender in the
`from` field) will be reduced according to the gas rules of the EVM
once your transaction makes it into a block. After some time, your
transaction should appear included in a block confirming that the
state it brought about is a consensus. Your contract now lives on the
blockchain.

The asynchronous way of doing the same looks like this:

``` {.sourceCode .js}
MyContract.new([arg1, arg2, ...,]{from: primaryAccount, data: EVMCode}, function(err, contract) {
  if (!err && contract.address)
    console.log(contract.address);
});
```

Interacting with a contract
---------------------------

Interaction with a contract is typically done using an abstraction
layer such as the
[eth.contract()](https://github.com/Ledgerium/wiki/wiki/JavaScript-API#web3ethcontract)
function which returns a javascript object with all of the contract
functions available as callable functions in javascript.

The standard way to describe the available functions of a contract is
the [ABI
definition](https://github.com/Ledgerium/wiki/wiki/Ledgerium-Contract-ABI).
This object is an array which describles the call signature and return
values for each available contract function.

``` {.sourceCode .js}
var Multiply7 = eth.contract(contract.info.abiDefinition);
var myMultiply7 = Multiply7.at(address);
```

Now all the function calls specified in the ABI are made available on
the contract instance. You can just call those methods on the contract
instance in one of two ways.

``` {.sourceCode .js}
myMultiply7.multiply.sendTransaction(3, {from: address})
"0x12345"
myMultiply7.multiply.call(3)
21
```

When called using `sendTransaction` the function call is executed via
sending a transaction. This will cost ether to send and the call will
be recorded forever on the blockchain. The return value of calls made
in this manner is the hash of the transaction.

When called using `call` the function is executed locally in the EVM
and the return value of the function is returned with the function.
Calls made in this manner are not recorded on the blockchain and thus,
cannot modify the internal state of the contract. This manner of call
is referred to as a **constant** function call. Calls made in this
manner do not cost any ether.

You should use `call` if you are interested only in the return value
and use `sendTransaction` if you only care about *side effects* on the
state of the contract.

In the example above, there are no side effects, therefore
`sendTransaction` only burns gas and increases the entropy of the
universe.

Contract metadata
-----------------

In the previous sections we explained how you create a contract on the
blockchain. Now we will deal with the rest of the compiler output, the
**contract metadata** or contract info.

When interacting with a contract you did not create you might want
documentation or to look at the source code. Contract authors are
encouraged to make such information available by registering it on the
blockchain or through a third party service, such as
[EtherChain](https://www.etherchain.org/contracts). The `admin` API
provides convenience methods to fetch this bundle for any contract
that chose to register.

``` {.sourceCode .js}
// get the contract info for contract address to do manual verification
var info = admin.getContractInfo(address) // lookup, fetch, decode
var source = info.source;
var abiDef = info.abiDefinition
```

The underlying mechanism that makes this work is is that:

-   contract info is uploaded somewhere identifiable by a *URI* which
    is publicly accessible
-   anyone can find out what the *URI* is only knowing the contracts
    address

These requirements are achieved using a 2 step blockchain registry.
The first step registers the contract code (hash) with a content hash
in a contract called `HashReg`. The second step registers a url with
the content hash in the `UrlHint` contract. These [registry
contracts](https://github.com/Ledgerium/go-Ledgerium/blob/develop/common/registrar/contracts.go)
were part of the Frontier release and have carried on into Homestead.

By using this scheme, it is sufficient to know a contract's address to
look up the url and fetch the actual contract metadata info bundle.

So if you are a conscientious contract creator, the steps are the
following:

1.  Deploy the contract itself to the blockchain
2.  Get the contract info json file.
3.  Deploy contract info json file to any url of your choice
4.  Register codehash -\content hash -\url

The JS API makes this process very easy by providing helpers. Call
`admin.register` to extract info from the contract, write out its json
serialisation in the given file, calculates the content hash of the
file and finally registers this content hash to the contract's code
hash. Once you deployed that file to any url, you can use
`admin.registerUrl` to register the url with your content hash on the
blockchain as well. (Note that in case a fixed content addressed model
is used as document store, the url-hint is no longer necessary.)

``` {.sourceCode .js}
source = "contract test { function multiply(uint a) returns(uint d) { return a * 7; } }"
// compile with solc
contract = eth.compile.solidity(source).test
// create contract object
var MyContract = eth.contract(contract.info.abiDefinition)
// extracts info from contract, save the json serialisation in the given file,
contenthash = admin.saveInfo(contract.info, "~/dapps/shared/contracts/test/info.json")
// send off the contract to the blockchain
MyContract.new({from: primaryAccount, data: contract.code}, function(error, contract){
  if(!error && contract.address) {
    // calculates the content hash and registers it with the code hash in `HashReg`
    // it uses address to send the transaction.
    // returns the content hash that we use to register a url
    admin.register(primaryAccount, contract.address, contenthash)
    // here you deploy ~/dapps/shared/contracts/test/info.json to a url
    admin.registerUrl(primaryAccount, hash, url)
  }
});
```

Testing contracts and transactions
----------------------------------

Often you need to resort to a low level strategy of testing and
debugging contracts and transactions. This section introduces some
debug tools and practices you can use. In order to test contracts and
transactions without real-word consequences, you best test it on a
private blockchain. This can be achieved with configuring an
alternative network id (select a unique integer) and/or disable peers.
It is recommended practice that for testing you use an alternative
data directory and ports so that you never even accidentally clash
with your live running node (assuming that runs using the defaults.
Starting your `geth` with in VM debug mode with profiling and highest
logging verbosity level is recommended:

``` {.sourceCode .bash}
geth --datadir ~/dapps/testing/00/ --port 30310 --rpcport 8110 --networkid 4567890 --nodiscover --maxpeers 0 --vmdebug --verbosity 6 --pprof --pprofport 6110 console 2~/dapp/testint/00/00.log
```

Before you can submit any transactions, you need set up your private
test chain. See test-networks.

``` {.sourceCode .js}
// create account. will prompt for password
personal.newAccount();
// name your primary account, will often use it
primary = eth.accounts[0];
// check your balance (denominated in ether)
balance = web3.fromWei(eth.getBalance(primary), "ether");
```

``` {.sourceCode .js}
// assume an existing unlocked primary account
primary = eth.accounts[0];

// mine 10 blocks to generate ether

// starting miner
miner.start(4);
// sleep for 10 blocks (this can take quite some time).
admin.sleepBlocks(10);
// then stop mining (just not to burn heat in vain)
miner.stop();
balance = web3.fromWei(eth.getBalance(primary), "ether");
```

After you create transactions, you can force process them with the
following lines:

``` {.sourceCode .js}
miner.start(1);
admin.sleepBlocks(1);
miner.stop();
```

You can check your pending transactions with:

``` {.sourceCode .js}
// shows transaction pool
txpool.status
// number of pending txs
eth.getBlockTransactionCount("pending");
// print all pending txs
eth.getBlock("pending", true).transactions
```

If you submitted contract creation transaction, you can check if the
desired code actually got inserted in the current blockchain:

``` {.sourceCode .js}
txhash = eth.sendTansaction({from:primary, data: code})
//... mining
contractaddress = eth.getTransactionReceipt(txhash);
eth.getCode(contractaddress)
```

