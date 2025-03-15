# Signals Publisher

 - [take me there now](action:SignalsPublisher)
 
The **Signals Publisher** tool lets you publish Strategy signals to a Signal Publishing Service, such as [Collective2.com](https://www.collective2.com) or the [Wealth$im](https://www.wealth-lab.com/WealthSim) simulated trading feature on WealthLab.com.
 - **Collective2** allows you to offer your Signals to other users for a monthly subscription fee.
 - The **Wealth$im** service on WealthLab.com lets you build up a track record of trading Signals. In the future it will also allow you to offer your Signals to other WealthLab.com users for a weekly fee.

> For a demonstration, see this video on our YouTube Wealth-Lab Support channel: 
[![Revamped Signals Publisher](http://img.youtube.com/vi/S8fRB9v0F3c/0.jpg)](https://www.youtube.com/watch?v=S8fRB9v0F3c&t=326s "Signals Publisher") 

## Linking Strategies
The Signals Publisher works by establishing a link to a **Remote Strategy** on the selected Publishing Service, and a local **WL8 Strategy**. To create this link, drag and drop a Strategy from the WL8 Strategies tree into the tool.

## Configuring a Strategy
You **Configure** a Strategy when you first establish the Link, and then again when you select the Configure button or right click option. The configuration dialog is divided into two sections.

### Remote Service Setup
Here you select which remote **Publishing Service** to link to, and its corresponding **Remote Strategy**. Some Publishing Services require you log in before being able to select the Remote Strategy.

 - **Collective2** requires login, and then lets you select one of the Strategies you've previously created as the Remote Strategy. You'll need your Collective2 v4 API key which you can obtain [here](https://collective2.com/apikey). WealthLab uses your API key to log in.  
 - **WealthSim** uses your WealthLab user account info, so no login is required. There is only one Remote Strategy available, which represents your single account, but you can link multiple WL8 Strategies.

### WL8 Strategy Setup
In this section you configure the backtest settings of the WL8 Strategy. The Signals Publisher runs a backtest of your Strategy using these settings, and then publishes the resulting Signals to the Publishing Service. You control the backtest **Start Date**, **DataSet**, and **Position Size**.

If you select a Percent of Equity Position Size, the Signals Publisher will use the current equity reported by the Publishing Service for position size calculation.

---
## Running Strategies (Submitting Signals)
Click the **Run Strategy** button/menu item to run the Strategy and submit the resulting Signals to the associated Publishing Service. Kicking off this process starts a backtest of the linked WL8 Strategy, and the resulting Signals are synchronized with the open positions reported by the Remote Strategy.

Use the **Manage Signals** link on the toolbar to navigate to the web site on the Publishing Service for managing the Strategy Signals there.

---
## Automatically Submitting Signals 
Use the command-line switch **/P** to open Signals Publisher and automatically Publish all Strategies. To set up automatic publishing at a specific time of day, use the procedure outlined in the [Scheduled Update topic](ScheduledUpdateTab), but adding or using the **/P**
switch.