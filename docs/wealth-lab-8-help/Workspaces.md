# Workspaces
The **Workspaces** option in the main menu lets you work with window Workspaces.  A **Workspace** preserves the configuration of all windows that are currently open. When you **save** a Workspace, a new menu item is added containing the name you provide. When you select that menu item, the corresponding Workspace loads. You can **delete** a **Workspace** by selecting the red X next to the name in a Workspace menu item.

**Auto-Run Strategies when Workspaces Open**  
Enable this option in the **Workspaces** menu to automatically run backtests for Strategy Windows saved with a Workspace. 

**Load Workspaces from the Command Prompt or Task Scheduler**  
Use the **/w** switch to launch Wealth-Lab with a pre-determined Workspace.   

%{color:blue}**Example**% 
```
"C:\Program Files\Quantacula, LLC\WealthLab 8\WealthLab8.exe" /w "Workspace Name"
```
*The use of quotes is required when the pathname or Workspace name contains spaces.* 

For all command line arguments, see the [Command Line Arguments](CommandLineArguments) topic. 

%{color:blue}**Important!**% 
> Loading a saved Workspace will replace all Wealth-Lab windows that are currently open. To load another Workspace without disturbing the current one, launch a new instance of Wealth-Lab and load the Workspace there. 

%{color:blue}**Notes: **% 
- Use **File > New Main Window** to open more than one Main Window.  A Workspace will preserve the configuration of all Main and Child Windows.
- Workspaces will recall the [Streaming Provider](StreamingProviders) saved with Strategy Windows and Strategy Monitor configurations.
- Use a Workspace to save your [Strategy Monitor](StrategyMonitor), [Strategy Rankings](StrategyRankings), and [Quotes](Quotes) configurations. 
- You can enable [Strategies](Strategy) from a Workspace to **automatically execute** after a Workspace has opened, by enabling **Auto-Run Strategies When Workspaces Open** in the Workspaces menu. 
- You can enable Strategies that were active in [Strategy Monitor](StrategyMonitor) windows to **reactivate** after a Workspace has opened by **Auto-Reactivate Strategy Monitor When Workspaces Open** in the Workspaces menu. 
