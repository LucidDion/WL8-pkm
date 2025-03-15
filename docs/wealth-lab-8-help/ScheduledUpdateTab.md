
# Update Log/Scheduled Update

Use this simple interface to enable and update all checked **Historical** and **Event Providers**.  Set a local time for the update.  The log for the latest update is shown on the left side. 

**Important!**
Scheduled Data Updates only request data for symbols and scales that *already exist* in the local cache.  You must request data for each symbol and scale in a chart, strategy, or using the DataSets tab at least once for scheduled updates to work.

%{color:blue}**Note!**% 
> This Data Manager tab must be open for the scheduled update to occur.

---
## Task Scheduler Update
The Windows Task Scheduler can launch Wealth-Lab, run the update, and even close the application when the update is complete. This method and its "switches" are independent of the *Schedule a Data Update* checkbox and time shown in this view, however, you still must have checked all **Historical** and **Event Providers** 
that you wish to update. 

**Procedure:**
1. Open the Task Scheduler.  For example, press the Windows key + R to open the Run box. Type  **taskschd.msc**  and press Enter.
2. Create/Select the folder in which you want to create the update task, right click the folder, and select **Create Basic Task...**
3. Give it a Name and Description, then click **Next**. 
4. **Trigger** - we recommend you select **Weekly**, and in the **Next** step select the time for the update and mark each day required. 
5. **Action** - select **Start a program**, and then **Next**. 
6. **Browse...** to locate the Wealth-Lab 8 installation directory and select **WealthLab8.exe**. 
7. **Add arguments:**  
**/U (required)** to perform the update  
**/C (optional)** to close Wealth-Lab when the update completes. Leave a space between /U and /C
8. Click **Finish**

Your computer needs to be running for scheduled tasks to run!
