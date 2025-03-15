## Equity

The equity curve portrays the Strategy's performance over the historical backtesting period, optionally compared to Buy and Hold. In portfolio backtests, the amount of exposure taken by the Strategy is also represented. 
 
The Equity Curve graph contains the following components:

**Account Equity**  
Account Equity is portrayed as the solid green area of the graph. Equity changes over time as 
trading-system Positions gain or lose value.  The Account Equity area itself is divided into a 
Cash Position (light green) and a Market Position (dark green). Dividing the Equity into Cash 
and Market levels lets you see at a glance the history of your strategy's market exposure.

**Benchmark Equity**  
The Buy & Hold Equity is represented as a black line calculated by taking a position in the Benchmark symbol at the beginning of the simulation period and holding it until the end of the backtest period. The Strategy Window uses real-world rules for the Benchmark position by basing its size on the closing value of the first bar of data (bar #0) and activating the Position at the opening price of the next bar. For futures the n  Because of this you'll notice that Benchmark Exposure is usually never exactly 100%, but is typically within 1% of 100%, assuming 1:1 margin.

**Long and Short Equity Lines**  
When activated by a button, the Long and Short Equity lines show the Account Equity for the long and short sides of the strategy, respectively.

**Equity Moving Average**  
When activated by a button, the 50-period simple moving average of the Equity curve is displayed on the chart as a blue line.

**Exploring the Equity Curve**  
You can zoom into any area of the Equity Curve by dragging a box (upper left to lower right) around the area with your mouse.  While zoomed in, use the right mouse button (click and drag) to navigate within the enlarged Equity Curve graph.  To return the Equity Curve to its normal size and position, draw a reverse box with the left mouse button by starting at the lower right corner and dragging to the upper left corner. By right clicking and dragging, you can manually center the graph.  

In addition, hovering the mouse pointer over a curve will display its date and precise dollar value. 

 
