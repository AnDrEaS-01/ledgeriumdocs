Quorum
======
## <a name="1"></a>What is Quorum?
Quorum is an Ethereum-based distributed ledger protocol that has been developed to provide the Financial Services Industry with a permissioned implementation of Ethereum that supports transaction and contract privacy.  

Quorum includes a minimalistic fork of the Go Ethereum client (a.k.a geth), and as such, leverages the work that the Ethereum developer community has undertaken.  
 
The primary features of Quorum, and therefore extensions over public Ethereum, are:

* Transaction and contract privacy
* Multiple voting-based consensus mechanisms
* Network/Peer permissions management
* Higher performance

Quorum currently includes the following components:

* Quorum Node (modified Geth Client)
* Constellation/Tessera - Transaction Manager
* Constellation/Tessera - Enclave

Whilst Quorum has been designed with Financial Services use cases in mind, its implementation is not Financial Services specific and hence is appropriate for other industries that are interested in utilizing Ethereum but require the above primary features.

### Background Reading
For more information on the design rationale and background to Quorum, please read the [**Quorum Whitepaper**](https://github.com/jpmorganchase/quorum-docs/blob/master/Quorum%20Whitepaper%20v0.1.pdf), view the [Hyperledger deck](https://drive.google.com/open?id=0B8rVouOzG7cOeHo0M2ZBejZTdGs) or watch the [presentation](https://drive.google.com/open?id=0B8rVouOzG7cOcDg4UkxqdTBacm8) given to the Hyperledger Project Technical Steering Committee meeting on 22-Sept-16.


## <a name="2"></a>Logical Architecture Diagram
[[https://github.com/jpmorganchase/quorum-docs/blob/master/images/Quorum%20Architecture.JPG]]

## <a name="3"></a>Component Overview
### Quorum Node
The Quorum Node is intentionally designed to be a lightweight fork of geth in order that it can continue to take advantage of the R&D that is taking place within the ever growing Ethereum community.  To that end, Quorum will be updated in-line with future geth releases.

The Quorum Node includes the following modifications to geth:
 1. Consensus is achieved with the Raft or Istanbul BFT consensus algorithms instead of using Proof-of-Work.
 2. The P2P layer has been modified to only allow connections to/from permissioned nodes.
 3. The block generation logic has been modified to replace the ‘global state root’ check with a new ‘global public state root’.
 4. The block validation logic has been modified to replace the ‘global state root’ in the block header with the ‘global public state root’
 5. The State Patricia trie has been split into two: a public state trie and a private state trie.
 6. Block validation logic has been modified to handle ‘Private Transactions’
 7. Transaction creation has been modified to allow for Transaction data to be replaced by encrypted hashes in order to preserve private data where required
 8. The pricing of Gas has been removed, although Gas itself remains

### Constellation & Tessera
[Constellation](https://github.com/jpmorganchase/constellation) and [Tessera](https://github.com/jpmorganchase/tessera) are Haskell and Java implementations of a general-purpose system for submitting information in a secure way. They are comparable to a network of MTA (Message Transfer Agents) where messages are encrypted with PGP. It is not blockchain-specific, and are potentially applicable in many other types of applications where you want individually-sealed message exchange within a network of counterparties. The Constellation and Tessera modules consist of two sub-modules: 
* The Node (which is used for Quorum's default implementation of a `PrivateTransactionManager`) 
* The Enclave


#### Transaction Manager
Quorum’s Transaction Manager is responsible for Transaction privacy.  It stores and allows access to encrypted transaction data, exchanges encrypted payloads with other participant's Transaction Managers but does not have access to any sensitive private keys. It utilizes the Enclave for cryptographic functionality (although the Enclave can optionally be hosted by the Transaction Manager itself.)

The Transaction Manager is restful/stateless and can be load balanced easily.

For further details on how the Transaction Manager interacts with the Enclave, please see the [[Transaction Processing & Privacy| Transaction Processing]] page.

#### The Enclave

Distributed Ledger protocols typically leverage cryptographic techniques for transaction authenticity, participant authentication, and historical data preservation (i.e. through a chain of cryptographically hashed data.)  In order to achieve a separation of concerns, as well as to provide performance improvements through parallelization of certain crypto-operations, much of the cryptographic work including symmetric key generation and data encryption/decryption is delegated to the Enclave.  

The Enclave works hand in hand with the Transaction Manager to strengthen privacy by managing the encryption/decryption in an isolated way.  It holds private keys and is essentially a “virtual HSM” isolated from other components.

Again, for further details on the Enclave, please see the [[Transaction Processing & Privacy| Transaction Processing]] page.
