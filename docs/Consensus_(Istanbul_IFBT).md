Consensus (Istanbul IFBT)
=========================

With no need for POW/POS in a permissioned network, Quorum instead
offers multiple consensus mechanisms that are more appropriate for
consortium chains:

Raft-based Consensus: A consensus model for faster blocktimes,
transaction finality, and on-demand block creation. See Raft-based
consensus for Ledgerium/Quorum for more information Istanbul BFT
(Byzantine Fault Tolerance) Consensus: A PBFT-inspired consensus
algorithm with transaction finality, by AMIS. See Istanbul BFT Consensus
documentation, the RPC API, and this technical web article for more
information Clique POA Consensus: a default POA consensus algorithm
bundled with Go Ledgerium. See Clique POA Consensus Documentation and a
guide to setup clique json with puppeth
