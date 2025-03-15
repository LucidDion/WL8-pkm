# Building Blocks

 - [take me there now](action:BuildingBlockStrategy)

**Building Blocks** let you build a trading Strategy using drag and drop, no coding required. You drag **Entry**, **Exit**, and **Condition** **Blocks** onto the design surface of a [Building Block Strategy](BuildingBlock) to compose your Strategy's trading logic. 

Building Blocks can also be used to get a jump start to coding, because you can convert a Building Block strategy to a C# Coded strategy . That can be helpful for those who want to learn how to code strategies.

---

## Building Block Rules
There are a few simple rules to keep in mind when composing your Building Block Strategy:

 - Each **Entry Block** needs at least one corresponding (Buy/Sell, Short/Cover) **Exit Block** somewhere beneath it.
 - If there are more than one **Exit Block** beneath an **Entry Block**, each **Exit Block** will apply. For example, you can drop both a **Profit Target** and a **Stop Loss** Exit Block under an **Entry Block**.
 - You can drop one or more **Condition Blocks** onto an **Entry** or **Exit Block**. The entries and exits will not trigger unless *all of* the conditions are satisfied.
 - If you want to compose an *"or"* style condition, drop two **Exit Blocks** under the same **Entry Block**, and attach a separate **Condition Block** to each **Exit**.

 [![OR Divider](http://img.youtube.com/vi/RxikkJgQk8Y/0.jpg)](http://www.youtube.com/watch?v=RxikkJgQk8Y&t=83s "OR Divider")

 --- 

## Building Blocks Roster
The following pages describe the various Building Blocks available:
 - [Entry and Exit Blocks](EntryAndExitBlocks)
 - [Condition Blocks](ConditionBlocks)
 - [Multi-Condition Groups and the OR Divider](MultiConditionGroup)
 - [Qualifier Blocks](QualifierBlocks)

 ---

## Position Management
At the top of the Building Block Strategy Designer you'll find a selection for **Position Management** with the following two options, and this selection applies to *each **Entry Block** in your Strategy*. 

 - Single Position (default)
 - Multiple Position
 
 **Single Position** - each entry block can add *one active position per symbol*.  
 Most strategies have one entry block, which will limit the strategy to one Position per symbol. If, for example, the Strategy has BuyAtMarket *and* BuyAtLimit blocks, each one can control one Position. This makes it possible to have 2 active positions for the same symbol even with *Single Position*.

**Multiple Positions** - each entry block can add *many active positions per symbol*.  
A new Position will be added *whenever its Conditions are met*. This can be useful for Conditions such as Crossover/under and Turns up/down, rather than straight comparison Conditions, to scale in many positions per symbol. 

---

## Requesting new Building Blocks
If you have an idea for a new Building Block you would like to see, post it on the [Wealth-Lab web site discussion forums](https://www.wealth-lab.com/Discussions).  We review the forums and will implement requested Building Blocks on an ongoing basis.
