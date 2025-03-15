# Developing Extensions

[Extensions](Extensions) are implemented as **.NET classes**, and compiled into a **.NET class library**.  
You can create an **Extension** by using an external development tool such as 
[Microsoft Visual Studio 2022](href="https://www.visualstudio.com) or [SharpDevelop](http://www.icsharpcode.net).

## Creating a Class Library

 1. Be sure your project targets **.NET 6.0**. 
 2. Add a references to the <b>Wealth-LabCore</b> and <b>Wealth-LabData</b> class libraries, located in your  Wealth-Lab installation folder. Depending on the type of extension you are building, you may need to add more  references. These will be described in the various extension API articles.

![Target .NET 6.0](https://www.wealth-lab.com/images/WLHelp/TargetDotNet60.png)

## Using your Extension
To use your **Extension** in Wealth-Lab, simply copy its DLL into the Wealth-Lab startup folder. The next time Wealth-Lab starts up, your **Extension** should be visible, pending any bugs or exceptions.

## Licensed Extensions
If you intend to license your **Extension**, be sure to provide an **AssemblyProduct** attribute, and add the following custom **LicensedExtension** (defined in Wealth-LabCore) attribute in your AssemblyInfo.cs file:
```csharp
[assembly: LicensedExtension(true)]
```
The **LicensedExtension** attribute has one bool parameter that indicates whether this is a free (true) or a paid (false) Extension. 

The licensing mechanism is keyed off the **AssemblyProduct** attribute of your assembly. Please coordinate with us so we can add your **AssemblyProduct** to our database to track usage of your extension. We can also help you if you want to sell your Extension, integrating right into the [Wealth-Lab MarketPlace](https://www.wealth-lab.com/Extension) at Wealth-Lab.com.

## Extensions API
Please see the [Extensions API on Wealth-Lab.com](https://www.wealth-lab.com/Support/ExtensionApi).

- [DataSetProvider](https://www.wealth-lab.com/Support/ExtensionApi/DataSetProvider)
- [EventDataProvider](https://www.wealth-lab.com/Support/ExtensionApi/EventDataProvider)
- [HistoricalDataProvider](https://www.wealth-lab.com/Support/ExtensionApi/HistoricalDataProvider)
- [IndicatorLibrary](https://www.wealth-lab.com/Support/ExtensionApi/IndicatorLibrary)
- [StreamingDataProvider](https://www.wealth-lab.com/Support/ExtensionApi/StreamingDataProvider)
