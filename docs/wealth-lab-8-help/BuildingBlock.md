# Building Block Strategies

 - [take me there now](action:BuildingBlockStrategy)

You create these [Strategies](Strategies) by dragging and dropping **Building Blocks** from the [Building Blocks tree](BuildingBlocks). There are four basic types of Building Blocks you'll use to compose your Strategy:

 - [Entries](EntryAndExitBlocks) - control when your **Strategy** enters a new position, either **long** (**Buy**) or **short** (**Short**).
 - [Exits](EntryAndExitBlocks) - control when your **Strategy** exits an open position, either **long** (**Sell**) or **short** (**Cover**).
 - [Conditions](ConditionBlocks) - can be dropped onto **Entry** and **Exit Blocks**. Conditions control when the entries and exits occur. For example, on an Indicator crossover or after a certain amount of time has past.
 - [Qualifiers](QualifierBlocks) - can be dropped onto **Condition Blocks**, and change how their logic is processed. For example, a qualifier can change the logic so that the condition has to occur a certain number of times before resolving to true.
## Building Block Tips
 - Each **Entry** is paired with each corresponding **Exit(s)** it finds beneath it until another entry block is encountered.
 - You can pair multiple **Exits** with a single **Entry** (for example, a profit target and a stop loss).
 - You can drop any number of **Conditions** onto an **Entry** or **Exit**.
 - You can drop only one **Qualifier** onto a **Condition**.
 - You can build **Strategies** that use multiple **Entries**. These **Entries** can pair with the same, or different, **Exits**.

### Power Tip! - Duplicate Condition Blocks 
Copy fully configured Condition and/or MultiCondition Group blocks to the same or different signal block using a typical windows shortcutL Press and hold the Ctrl Key, then left click and drag the block to another signal block location. Configure the new block as required!

## Building Block Descriptions
See [Building Blocks](BuildingBlocks) for a detailed description of the available Blocks.
