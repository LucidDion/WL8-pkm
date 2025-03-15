# ASCII Data

ASCII is a universal text document format, and many data vendors use ASCII format to store their data. ASCII data can come in a wide variety of formats, and Wealth-Lab is very flexible in its ASCII support.

ASCII DataSet specifications:

- Bar scale and interval are recognized automatically.
- Each file contains data for one security only.
- All files for the same DataSet must be in the same folder and use the same file extension (e.g., .txt, .csv, ...).  
- The name of the file (excluding the extension) is used as the symbol. 
- Each record in the file represents one bar (or tick). 
- At a minimum, a record must contain a Date field and one numeric field (Close). 
- Excluding fields that are specified as Date, Time, or Security Name, all other fields must be numeric.  If your data files contain other fields that non-numeric, these fields should be specified as "Filler" when creating the ASCII DataSet in Wealth-Lab. 
- The format of each record (decimal character, field delimiter, etc.) is variable, but you must specify these properties when creating the ASCII DataSet in Wealth-Lab. See *Format Options* below.  
- Data can be in chronological or reverse-chronological order.  

## How to: Create an ASCII DataSet

**Step 1. Location and File Extension**

Navigate to the folder that contains the ASCII files. Next, specify the File Extension of your data files. When you change the file extension, the list of files is updated to show only the files that match the extension that you specified.

You can type your own File Extension if it isn't included in the drop down list. 
 
**Step 2. Specify the ASCII Format**

Specify the format of the data in your ASCII files. You must precisely specify how the data is arranged so that it can be parsed by the ASCII provider. To get an idea of how the data is arranged, click "Open first ASCII file in Notepad".
 
- *Field Order* &nbsp; Drag the fields to move data fields up or down. If the ASCII DataSet doesn't contain a data element, such as Volume, click on the item and delete it by clicking the "Remove Field".  Likewise, use the "Add Field" button to add to the Field Order and then move it to the appropriate position. 
- *Time* &nbsp; If the data file contains a separate field for time, add Time to the field list and move it to the appropriate position.  It's common for a single white space to appear between Date and Time.  In this case, don't add a separate Time field unless the Field Separator is actually  a "Space".
- *Filler Items* &nbsp; For non-numeric items, or other fields that should not be read, add "Filler" items to act as place holders. Filler fields are simply skipped so that the rest of file can be properly parsed.
- *Named Series* &nbsp; They contain any other numerical data like indicators or fundamentals. You must provide a unique name for each custom field that you enter. Use the *NamedSeries* method of the [BarHistory] object to access a Custom Field's DataSeries.

**Format Options**
 
- *Date Format* &nbsp; Specifies the description of how dates are formatted in the file.  For a specification of the Date and Time Format specifiers, refer to:
	* [Standard date and time format strings](https://docs.microsoft.com/en-us/dotnet/standard/base-types/standard-date-and-time-format-strings)
	* [Custom date and time format strings](https://docs.microsoft.com/en-us/dotnet/standard/base-types/custom-date-and-time-format-strings)
- *Time Format* &nbsp; Specifies the description of how time values (if present) are formatted in the file.
- *Field Delimiter* &nbsp; Specifies the character that separates the fields in a single row of data. If your ASCII data uses a field separator that doesn't appear in the list, just type it in. 
- *Decimal Character* &nbsp; Specifies which character is used as the decimal separator for price fields - either Period (.) or Comma (,).
- *Number of Header/Footer Lines* &nbsp; If your data file contains one or more header/footer lines, specify this value in the respective  field. These lines are ignored when the file data is imported.

> *Hint*: frequently used ASCII formats can be saved in presets which is convenient for later reuse. Click *-None-* to reset the dialog.

[![Saved ASCII Formats](http://img.youtube.com/vi/RxikkJgQk8Y/0.jpg)](http://www.youtube.com/watch?v=RxikkJgQk8Y&t=23s "Saved ASCII Formats")

 
**Step 3. Data Preview**

The next step validates that the ASCII Format was correctly specified.  If it was, you'll see a sample of your file's data in the preview window. Otherwise, a Parse Error dialog will indicate where an error was detected.  In this case, go back and correct the problem.

## ASCII Data Cache

Because ASCII files contain text strings, they have to be parsed and converted to numbers. Binary files, like WL native format, MetaStock and others don't require parsing, so working with them is faster. Caching ASCII data speeds up working with huge **intraday** files by reducing file access time. 

When an ASCII file is accessed for the first time, a binary file is created that comprises its BarHistory object and any custom TimeSeries that it contains. Subsequent backtests benefit from reading the data from binary cache. The provider compares the time of last modification of actual ASCII file with its cached version. If it hasn't been modified, data is read from cache, otherwise the cache is cleared and re-created.

