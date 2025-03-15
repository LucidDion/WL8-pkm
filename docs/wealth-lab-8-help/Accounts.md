# Accounts

 - [take me there now](action:Accounts)

### Accounts Window Overview
The Accounts Window provides balance and positions information for each account associated with a connected Broker. Wealth-Lab 8 supports multiple simultaneous Broker connections. When you open the Account Window, WL8 will attempt to auto-connect to any installed Broker(s). Brokers that fail to connect may need to be configured in the [Order Manager](OrderManager) first.

### Balances
The balances that appear below each account tile come directly from the Broker, and the fields you see here might include some that are Broker-specific. The last line contains a summary of the open positions reported by the Broker, including their total value and profit.

### Positions
The bulk of the Accounts Window is occupied by a list of open positions that were reported by the connected Broker(s). You can hide positions from a specific Broker by clicking the "eye" icon in the Broker's tile.

### Excluding an Account from Trading Thresholds
When you enable this option for an account, it will no longer participate in **Trading Thresholds** defined in the [Data/Trading Preferences](DataPreferences). This means that the account will not be considered when checking the Trading Thresholds, and any active entry orders will not be canceled if a Trading Threshold is hit.

### Updating Balances and Positions
Click the **Update** button in the toolbar to update the information. This causes a call to be made to each connected Broker. The responses from the Broker(s) are populated in the Broker tiles and positions list as they are received.
### Closing Positions
You can **Close Positions** by clicking one of the toolbar buttons, or the right click menu items. This places exit orders to close the selected position(s) in the list. View the [Order Manager](OrderManager) to see any new orders created. Use the **Flatten Account(s)** feature to place exit orders for all reported open positions in the selected Broker(s). Finally, use **Flatten Broker(s)** to place exit orders for all open positions in *all accounts* of the selected Broker(s).
### Streaming Updates
Click the **Streaming Updates** check box to stream live quotes into the **Current Price** field for each open position. Each Broker can be configured to use a different Streaming Provider. Be sure to set up the desired Streaming Provider(s) for each Broker before turning on streaming.
### Account Nicknames
Each account can be given a nickname to help identify multiple accounts by single broker. Click on the "..." button next to the account you'd want to assign a nickname to specify it in a popup dialog.