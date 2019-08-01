RPC
===

In previous sections we have seen how contracts can be written, deployed
and interacted with. Now it's time to dive into the details of
communicating with the Ledgerium network and smart contracts.

An Ledgerium node offers a
[RPC](https://wikipedia.org/wiki/Remote_procedure_call) interface. This
interface gives Ðapp's access to the Ledgerium blockchain and
functionality that the node provides, such as compiling smart contract
code. It uses a subset of the [JSON-RPC
2.0](http://www.jsonrpc.org/specification) specification (no support for
notifications or named parameters) as the serialisation protocol and is
available over HTTP and IPC (unix domain sockets on linux/OSX and named
pipe's on Windows).

If you are not interested in the details but are looking for an easy to
use javascript library you can skip the following sections and continue
with looking up Web3
