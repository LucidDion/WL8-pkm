## Tick-Based Historical Data
Wealth-Lab supports historical tick data using the following scales:
 - **Tick** - creates a bar based on specified number of ticks
 - **Second** - creates a bar based on specified number of seconds
 - **Volume** - adds ticks to a bar until a specified volume threshold reached

Some Historical Providers (IQFeed, Interactive Brokers, for example) support historical tick data. Tick data is downloaded and stored locally on a day-by-day basis, and used to generate the historical bar data for the scales mentioned above.
