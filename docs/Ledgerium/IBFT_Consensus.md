# Consensus
While Quorum supports Raft-based, Clique POA and IBFT Consensus algorithm, Ledgerium Blockchain adopted Quorum's IBFT (Istanbul Byzantine Fault Tolerance) to build it blockchain. 

**IBFT (Istanbul Byzantine Fault Tolerant)** is a consensus mechanism which is an alternative to Proof of Work in an Ethereum network. Like other algorithms, IBFT ensures a single, agreed-upon ordering for transactions in the blockchain, and provides added benefits for enterprises, including settlement finality. IBFT was first implemented in Geth by Amis Technologies, and later adopted in Quorum.

The PoW (Proof of Work) algorithm is famously costly, in both hardware and electricity. This cost is intentional, to prevent anyone from easily taking over the network, and so while PoW has been pioneer for building full decentralization where anyone (including attackers) can participate, the alternate algorithm has to be evaluated.

The PoS (Proof of Stake) algorithm scores over PoW in terms of hardware and electricity consumption. The creator of the next block is chosen via various combinations of random selection and wealth or age (i.e., the stake), however it plagues with one issue i.e. the "nothing-at-stake" problem, wherein block generators have nothing to lose by voting for multiple blockchain histories, thereby preventing consensus from being achieved. 

The PoA (Proof of Authority) emerges as a possible best solution, utilizing a system whereby nodes in the network are allocated the privilege of producing new blocks for the chain using a round-robin or other arbitrary system. IBFT is one of the many flavours of PoA.

## **Key Advantages**  
- **Immediate block finality**  
  There’s only 1 block proposed at a given chain height. The single chain thus removes forking, uncle blocks, and the risk that a transaction may be “undone” once on the chain at a later time.

- **Reduced time between blocks**  
  The effort needed to construct and validate blocks is significantly reduced (in particular with respect to PoW), greatly increasing the throughput of the chain.

- **High data integrity and fault tolerance**  
  IBFT uses a group of validators to ensure the integrity of each block being proposed. A super-majority (~66%) of these validators are required to sign the block prior to insertion to the chain, making block forgery very difficult. The ‘leadership’ of the group also rotates over time — ensuring a faulty node cannot exert long term influence over the chain.

- **Operationally flexible**  
  The group of validators can be modified in time, ensuring the group contains only full-trusted nodes.

## **Consensus Model**
- IBFT uses a pool of validating nodes (**Validator**s) operating on an Ethereum network to determine if a proposed block is suitable for addition to the chain.

- One node of the **Validator**s is deterministically selected as the **Proposer** and is responsible for constructing a block at the block-interval and sharing said block with the group. If a super-majority of the **Validator**s deem the block to be valid it is added to the blockchain.

- At the completion of the consensus round, the **Validator**s may select a new **Proposer** which will be responsible for providing the candidate Block at the next block interval.

- The consensus mechanism is a synchronised state machine which is responsible for ensuring all **Validator**s append the same block to the chain at the same height.

- If a block fails to insert, the **Proposer** is changed, and the process starts anew.

- To ensure only one block can be appended to the state machine, IBFT prevents changing the proposed block once a super-majority of validators have agreed to its insertion. This process is referred to as ‘Block Locking’.

- The **IBFT** consensus mechanism offers system stability provided less than 1/3 of the validating nodes are behaving incorrectly (either due to being compromised or due to **faulty** code). I.e. to tolerate F **faulty** nodes the validation group must contain at least 3F + 1 nodes (more than this does not increase system integrity).
Note: Herein F implies the number of **faulty** nodes tolerated by the system.

## **Validation Group Membership**  
- The members of the validation group may change over time through a voting mechanism. Members can be added or removed through a majority (Floor(N/2) + 1) vote; each vote is captured in the Block Header.

- Each node in the network (including non-validating nodes) is responsible for tracking the vote tally for each **validator** to determine the current Validators and ensure signatures on mined blocks fall within the expected group.

- Given each vote is contained in the Block Header, only the **Proposer** for a given round is able to cast a vote. Thus it is important, if nodes are to be added/removed in a timely fashion, that the **Proposer** role be updated on a regular basis.

- Once a node reaches majority votes, they immediately join/leave the **validator** group.

- IBFT recognises a Voting Epoch, which defines a point at which all votes which have not yet reached a majority are removed, forcing the voting tally to be restarted. This implies when tallying votes, Validators need only start at the most recent epoch. By default, the Voting Epoch occurs every 30,000 blocks.

- Votes define a change of state (i.e. candidates get voted in, validators get voted out), not voting for a given node implies the **Validator** does not wish the node to change state (an explicit vote is not required to maintain the status quo).

