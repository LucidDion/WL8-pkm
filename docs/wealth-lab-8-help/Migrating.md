# Migrating from WL7 to WL8
You'll hopefully find the migration from WL7 to WL8 smooth, but there are a few changes that you might need to make to adapt Strategies from WL7 to WL8.

## Migration Tool
The first step would be to use the **Migration Tool** in the WL8 Home Page tool. This tool will migrate your **DataSets**, **Strategies**, and select user **Preferences**. After the migration is complete, WL8 will restart to utilize the new settings. During the migration, WL8 automatically performs a conversion of Strategy source code to account for the differences documented below.
![enter image description here](https://www.wealth-lab.com/images/WLHelp/Migration.png)

## Code Differences between WL7 and WL8
There are a few areas where Strategy code will need to be changed to run a WL7 Strategy in WL8.
### New Types to support a Cross Platform Library
Since the WealthLab.Core library is now cross-platform, it cannot include any Windows-specific references or classes. As such, we needed to refactor out uses of the Color and Font classes in WealthLab.Core. System.Drawing.Color has been replaced with a new **WLColor** class, which has largely the same interface. And System.Drawing.Font has been replaced with a **WLFont** class, which contains a few properties that describe the font in a cross platform way. The WL7 -> WL8 translator automatically makes these translations.
### Enumerated Types
According to [Microsoft .NET Coding Guidelines](https://docs.microsoft.com/en-us/previous-versions/dotnet/netframework-1.1/4x252001%28v=vs.71%29?redirectedfrom=MSDN), enumerated type names should be singular, unless that are decorated with the ```[Flags]``` attribute. We have adopted this style and so had to change many of the enum names. For example, **ParameterTypes** becomes **ParameterType**, and **PlotStyles** becomes **PlotStyle**. The WL7 to WL8 translation performs these replacements.
### Factories
WL8 contains a Factor class for any item that is discoverable at run-time, such as Historical Data Provider, Brokers, and Chart Drawing Objects. In WL7, each of these Factories is a standalone class, with its own method names like FindDataSet or FindDrawingObject. In WL8, we have a new generic base class **FactoryBase<T>** that all of the Factories derive from. Since static classes cannot be inherited, Factories are now non-static, but each has a singleton Instance property. They all share a common set of methods, but each specific Factory might introduce its own custom methods as needed. 

**FactoryBase<T>** has an **Items** property that contains all of the item instances for the target Type. It provides a **Find** method to locate an item by name (by matching the item's **Name** property.)

If you find youself using any of the Factories in your Strategy code, you'll need to make adaptations like the following:
```csharp
ScoreCardFactory.FindScoreCard(name)
```
becomes ...
```csharp
ScoreCardFactory.Instance.Find(name)
```
## Importing WL7 Strategies
You can import exported WL7 Strategies directly into WL8 using the normal mechanisms. WL8 will automatically perform the translation and save the imported Strategy in the new XML format.