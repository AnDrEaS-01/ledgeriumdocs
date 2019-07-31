Ledgerium Tools
===============

A tool for generating a docker-compose yaml for deploying N nodes with
IBFT consensus

Update initialparams.json
-------------------------

Edit this file before running the application

1.  mode: Change mode type (full/addon)

    > -   If mode type is full, this application will create a
    >     ledgeriumnetwork folder outside ledgeriumtools which has
    >     static-nodes and externalised genesis files.
    > -   If mode type is addon, get latest ledgeriumnetwork files from
    >     github and paste those files under ledgeriumtools/output/tmp

2.  externalIPAddress : To host a node for a network that can be
    connected to by anyone outside your LAN
3.  nodeName : Hostname of the machine where nodes will be hosted.
4.  domainName : Domain name of the external IP Address. domainName is
    needed for every node to which any client wants to send transactions
    or do “geth attach”

Run ledgeriumtools application
------------------------------

To start the application, run

-   node index.js

Takes input from the command line interface, prompts to enter number of
menmonics

-   Number of Mnemonics : 2
-   Enter Mnemonic 0 : ******\**********\********\****\****
-   Enter Password 0 : *******\********
-   Enter Mnemonic 1 : *********\************\********\****\***\*
-   Enter Password 1 : *******\********

Enter the Mnemonics and password which will generate the nodekeys and
password

The number of nodes brought up is equal to the number of keys/menmonics
provided in the file i.e. n keys signifies n nodes with the respective
keys as coinbase/etherbase

The docker file will be generated in the output folder.

Change directory to output and use

-   docker-compose up -d to start up the nodes
-   docker-compose down to bring down the nodes

Note :

-   This application is currently using constellation as the
    private transaction manager.\*
-   Don't use the -v option to bring down the nodes as the current
    blockchain data will be lost\*
-   For subsequent runs make sure the tmp dir created in output folder
    is deleted\*

