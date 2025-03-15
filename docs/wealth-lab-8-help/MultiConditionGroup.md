# Multi-Condition Groups and the OR Divider
## OR Divider
All of the [Condition Blocks](ConditionBlocks) in an [Entry/Exit Block](EntryExitBlocks) have their criteria logically **anded** together while processed. This means that all the Conditions must resolve to true for the Entry/Exit to trigger. The **OR Divider** is a special Block with lets you divide Conditions into groups. The Entry/Exit resolves to true if **any of** the Conditions groups resolve to true.

When you drop an OR Divider into a group of Conditions, it is placed under the Condition upon which it was dropped.

[![Nested Multi-Condition Groups](http://img.youtube.com/vi/RxikkJgQk8Y/0.jpg)](http://www.youtube.com/watch?v=RxikkJgQk8Y&t=278s "Nested Multi-Condition Groups")

OR Dividers cannot be dropped into a Multi-Condition Group, described next.

## Multi-Condition Groups
This special Building Block can be dropped onto an [Entry/Exit Block](EntryAndExitBlocks), or within another Multi-Condition Group. It provides a container to host multiple [Condition Blocks](ConditionBlocks), which you can drop inside. The Multi-Condition Group has two modes of operation, described below.

[![Multi-Condition Group Building Block](http://img.youtube.com/vi/ix8sAC-iu0k/0.jpg)](https://www.youtube.com/watch?v=ix8sAC-iu0k&t=283s "Multi-Condition Group Building Block")

---
## At Least N Conditions True

When this Group Type is selected, you specify the minimum number of Conditions that need to be true in order for the overall Group Condition to resolve to true. In this example, if two of the three oscillators are oversold, the overall Multi-Condition will resolve to true.
 
![At Least N Conditions MC Group](https://www.wealth-lab.com/Images/WLHelp/MCG1.png)

---
## Condition Number N is True
The second option instructs the Multi-Condition Group to resolve to true only if the specific 
numbered Condition Block is true. The first Condition Block is numbered 1. You may wonder why it would be useful to construct such a Multi-Condition Group, instead of just dropping the single desired Condition right onto the Entry/Exit. The payoff here comes when you make the How Many parameter optimizable. Then, during an [Optimization](Optimization), the optimizer will run through each of the Conditions, one by one, as the parameter is iterated. In the example below, an Optimization could determine which of the three oscillators performed best in the Strategy.
 
![Condition Number N is True MC Group](https://www.wealth-lab.com/Images/WLHelp/MCG2.png)