Full description with screenshots you can find on:
https://drive.google.com/file/d/1lL2y-Q-umMpYZEliZiQULXOqux1AcX0s/view?usp=sharing

# Problem statement:

Let's say that you are Elon Musk and you want to sell/buy 250 mio of Bitcoin.

If you would split 250 million USD into 25 trades each 10 million USD trade might have a market impact of around 1,3% (ex. Mid: 34 166, VWAP: 34 614). 

After each trade it is expected that the market will move against you, because you will not directly match interest on the other side, but you will in most cases execute with non-directional market makers that will be willing to close the position. After executing the first 50-70 million a lot of people would know that there is somebody on the market that is a heavy buyer/seller. Some people estimate that when Tesla sold 250 million USD worth of Bitcoin, market dropped 15%: 

Selling/buying a significant amount of crypto has significant influence on the market and final execution VWAP. It might be that the price slippage of selling 250 million would probably be between 5 and 10% (VWAP price vs. mid-market price from the beginning).
In case of Tesla that was holding $2.5 billion worth of bitcoin, selling 10% in would mean significant cost: $250 million worth of bitcoin sold with 7% price slippage = $17.5 million + decreases valuation of holding that are still owned by Tesla: $2.25 billion worth of bitcoin * 15% price impact = $337.5 million, giving a total estimated cost of $355 million.
Conclusion: To avoid any directional market movement influenced by bigger trades, one should find another party that is interested in another direction. Seeing the above example this was clearly hard to do for Tesla. 

# Product idea:

On one side we sign up buyers, on the other side we sign up sellers, at some point in time we do batch fixing where we match both sides using Uniwap v3 TWAP mid-rate calculated during the “locked” period.


## Notes for product implementation:

Assumptions:
1. Traders can wait for another counterparty that has opposite interest. 
2. Product is done for “bigger” deals in mind

There are 3 stages:
1. Find opposite interest
2. Agree on the price for the trade
3. Settle traders that has been matched

### Stage 2: Agree on the price for the trade

I am starting with the description of Stage 2, because it seems to be the most obvious one for me. 
Due to Smart Contract limitations related to: block processing times, MEV, Flash loans etc. it would make sense to use TWAP price from Uniswap v3 or some other established AMM platform based on Uniswap v2. Trades funds need to be “locked” during the TWAP period to avoid arbitrage. Duration of TWAP can be determined on a pair/pool basis.

### Stage 1&3: Find opposite interest & Settle traders that has been matched

Logic of Stage 1 is mostly determined by the way the settlement would work, so stage 1 should be considered together with stage 3.
The general idea is to let people sign up “up front” and wait for the match. The biggest issue is related to settlement and the fact that, when people sign up, the final rate is unknown. During the sign up period it is hard to determine how much of the coin1 pool will be matched with the coin2 pool. Some estimation can be done up front, but if the market would significantly move during TWAP measuring period the difference, who is matched and who is not will be significant. 

If we would have free gas & unlimited block size, the best way would be to use a Doubly Linked List to store information who is after who during settlement with ID that is always increasing. During the settlement process we would iterate through the list and define who is done/who is not done (ex. Users with ID smaller than 12 with USD are done, user 13 is done partially)

It would also allow users to withdraw funds before TWAP start time (ex. If a user that was second on the “sell ETH” would withdraw funds, user 1 and user 3 will be “linked”, ID 2 would not exist, sum funds on particular side would be updated). The issue is gas usage. According to the initial test, if there would be more than 700 users on one size, computation will be bigger than gas available in the block.

![image](https://user-images.githubusercontent.com/84227574/123256198-fc982100-d4f0-11eb-974a-72f45918e8c2.png)


Doable solution would be to put all people on one side to one basket and settle the % of the pull determined by the rate, but the user experience would be significantly reduced and it would not be fair that the guy that came last got the same “share” of the settlement as the guy that came first.

I was also thinking about some sort of “slots” with defined pool sizes to reduce gas usage in finding the place that got matched.

### Unsolved production definition issues:

How to do settlement (how it should work, who pays gas, how to do it, when, who is triggering it)
How to allow users to withdraw funds before the TWAP measuring period.
