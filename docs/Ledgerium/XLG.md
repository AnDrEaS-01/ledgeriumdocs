XLG
===

What is XLG?
------------

> Ledgerium is a hybrid chain, where validators are chosen based on
> various factors. Of all possible validators, 20% will always be
> maintained by ledgerium. 40% will be given to top universities and
> public institutions, and the remaining 40% will be given to
> enterprises or the open market. This will ensure at all times, we have
> 60% of validators locked and producing blocks, no matter what the
> value of the token is. Ether is the name of the currency used within
> Ledgerium. It is used to pay for computation within the LVM. This is
> done indirectly by purchasing gas for ether as explained in
> gas-and-ether.
>
> ### Denominations
>
> Ledgerium has a metric system of denominations used as units of ether.
> Each denomination has its own unique name (some bear the family name
> of seminal figures playing a role in evolution of computer science and
> cryptoeconomics). The smallest denomination aka *base unit* of ether
> is called Wei. Below is a list of the named denominations and their
> value in Wei. Following a common (although somewhat ambiguous)
> pattern, ether also designates a unit (of 1e18 or one quintillion Wei)
> of the currency.
>
>   ------------------------------------------------------------------------
>   Unit                   Wei Value  Wei
>   ---------------------- ---------- --------------------------------------
>   **wei**                1 wei      1
>
>   **Kwei (babbage)**     1e3 wei    1,000
>
>   **Mwei (lovelace)**    1e6 wei    1,000,000
>
>   **Gwei (shannon)**     1e9 wei    1,000,000,000
>
>   **microether (szabo)** 1e12 wei   1,000,000,000,000
>
>   **milliether           1e15 wei   1,000,000,000,000,000
>   (finney)**                        
>
>   **XLG**                1e18 wei   1,000,000,000,000,000,000
>   ------------------------------------------------------------------------
>
Obtaining XLG
-------------

> XLG is currently trading as an ERC-20 token. An initial supply of only
> 200 XLG was created out of which only 50% is currently in unlocked
> wallets. You can trade, buy or sell the ERC-20 XLG token on the
> following exchanges. Sending ether
>
> -   <https://acx.io/markets/xlgbtc>
> -   <https://idex.market/eth/xlg>

XLG supply
----------

> 200,000,000 XLG

XLG Wallet
----------

> The [Ledgerium
> Wallet](https://github.com/ledgerium-io/metamask-extention) supports
> sending ether via a graphical interface.
>
> Ether can also be transferred using the **geth console**.
>
> ``` {.sourceCode .console}
> > var sender = eth.accounts[0];
> > var receiver = eth.accounts[1];
> > var amount = web3.toWei(0.01, "ether")
> > eth.sendTransaction({from:sender, to:receiver, value: amount})
> ```
>
> For more information on ether transfer transactions, see
> account-types-gas-and-transactions.
>
> Ledgerium is unique in the realm of cryptocurrencies in that ether has
> utility value as a cryptofuel, commonly referred to as "gas". Beyond
> transaction fees, gas is a central part of every network request and
> requires the sender to pay for the computing resources consumed. The
> gas cost is dynamically calculated, based on the volume and complexity
> of the request and multiplied by the current gas price. Its value as a
> cryptofuel has the effect of increasing the stability and long-term
> demand for ether and Ledgerium as a whole. For more information, see
> account-types-gas-and-transactions.

Gas and ether
-------------

> -   <https://www.reddit.com/r/ethereum/comments/271qdz/can_someone_explain_the_concept_of_gas_in_ethereum/>
> -   <https://www.reddit.com/r/ethereum/comments/3fnpr1/can_someone_possibly_explain_the_concept_of/>
> -   <https://www.reddit.com/r/ethereum/comments/49gol3/can_ether_be_used_as_a_currency_eli5_ether_gas/>
>
> Gas is supposed to be the constant cost of network
> resources/utilisation. You want the real cost of sending a transaction
> to always be the same, so you can't really expect Gas to be issued,
> currencies in general are volatile.
>
> So instead, we issue ether whose value is supposed to vary, but also
> implement a Gas Price in terms of Ether. If the price of ether goes
> up, the Gas Price in terms of ether should go down to keep the real
> cost of Gas the same.
>
> Gas has multiple associated terms with it: Gas Prices, Gas Cost, Gas
> Limit, and Gas Fees. The principle behind Gas is to have a stable
> value for how much a transaction or computation costs on the Ledgerium
> network.
>
> -   Gas Cost is a static value for how much a computation costs in
>     terms of Gas, and the intent is that the real value of the Gas
>     never changes, so this cost should always stay stable over time.
> -   Gas Price is how much Gas costs in terms of another currency or
>     token like Ether. To stabilise the value of gas, the Gas Price is
>     a floating value such that if the cost of tokens or currency
>     fluctuates, the Gas Price changes to keep the same real value. The
>     Gas Price is set by the equilibrium price of how much users are
>     willing to spend, and how much processing nodes are willing to
>     accept.
> -   Gas Limit is the maximum amount of Gas that can be used per block,
>     it is considered the maximum computational load, transaction
>     volume, or block size of a block, and miners can slowly change
>     this value over time.
> -   Gas Fee is effectively the amount of Gas needed to be paid to run
>     a particular transaction or program (called a contract). The Gas
>     Fees of a block can be used to imply the computational load,
>     transaction volume, or size of a block. The gas fees are paid to
>     the miners (or bonded contractors in PoS).

