Below is a copy of:
https://drive.google.com/file/d/1lL2y-Q-umMpYZEliZiQULXOqux1AcX0s/view?usp=sharing

# Problem statement:

Let's say that you are Elon Musk and you want to sell/buy 250 mio of Bitcoin. Ex.: 

![image](https://user-images.githubusercontent.com/84227574/123254817-69aab700-d4ef-11eb-8324-8543acce09fb.png)
![image](https://user-images.githubusercontent.com/84227574/123254824-6c0d1100-d4ef-11eb-9a0f-2b64e768d783.png)


If you would split 250 million USD into 25 trades each 10 million USD trade might have a market impact of around 1,3% (ex. Mid: 34 166, VWAP: 34 614). 

![image](https://user-images.githubusercontent.com/84227574/123254857-75967900-d4ef-11eb-88de-187a5c2a6781.png)


On platforms like Uniswap it looks even worst:
![image](https://user-images.githubusercontent.com/84227574/123254908-8515c200-d4ef-11eb-94c6-99d95d41f537.png)


After each trade it is expected that the market will move against you, because you will not directly match interest on the other side, but you will in most cases execute with non-directional market makers that will be willing to close the position. After executing the first 50-70 million a lot of people would know that there is somebody on the market that is a heavy buyer/seller. Some people estimate that when Tesla sold 250 million USD worth of Bitcoin, market dropped 15%: 
![image](https://user-images.githubusercontent.com/84227574/123254936-8fd05700-d4ef-11eb-86b5-ef12e46d48e5.png)
![image](https://user-images.githubusercontent.com/84227574/123254945-9232b100-d4ef-11eb-851f-8f83e7d07042.png)

Selling/buying a significant amount of crypto has significant influence on the market and final execution VWAP. It might be that the price slippage of selling 250 million would probably be between 5 and 10% (VWAP price vs. mid-market price from the beginning).
In case of Tesla that was holding $2.5 billion worth of bitcoin, selling 10% in would mean significant cost: $250 million worth of bitcoin sold with 7% price slippage = $17.5 million + decreases valuation of holding that are still owned by Tesla: $2.25 billion worth of bitcoin * 15% price impact = $337.5 million, giving a total estimated cost of $355 million.
Conclusion: To avoid any directional market movement influenced by bigger trades, one should find another party that is interested in another direction. Seeing the above example this was clearly hard to do for Tesla. 

# Product idea:

On one side we sign up buyers, on the other side we sign up sellers, at some point in time we do batch fixing where we match both sides using Uniwap v3 TWAP mid-rate calculated during the “locked” period.

