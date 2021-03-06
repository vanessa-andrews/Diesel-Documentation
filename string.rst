String
======

String.Contains
---------------
Finds a substring inside an input string.

Overloads
~~~~~~~~~
1. **String.Contains(String inputString, String searchString, Bool ignoreCase, ICultureAccessor cultureAccessor): Bool**
2. **String.Contains(String inputString, String searchString, Bool ignoreCase): Bool**
3. **String.Contains(String inputString, String searchString): Bool**

- cultureAccessor defaults to the culture defined in settings
- ignoreCase defaults to false

Sample::

  String word = "bed";
  Bool containsCapitalE = String.Contains(word, "E");
  Bool containsE = String.Contains(word, "e", false);

String.CreateFile
---------------
Creates a file with fileName containing content.

Overloads
~~~~~~~~~
1. **String.CreateFile(String fileName, String content): File**

Sample::

  TextFile file = String.CreateFile("file.txt", "These are file contents");


String.EndsWith
---------------
Returns true if the search string ends with the input string, otherwise returns false. If ignore case is set to true, then case differences are disregarded when comparing the strings.

Overloads
~~~~~~~~~
1. **String.EndsWith(String inputString, String searchString, Bool ignoreCase, ICultureAccessor cultureAccessor): Bool**
2. **String.EndsWith(String inputString, String searchString, Bool ignoreCase): Bool**
3. **String.EndsWith(String inputString, String searchString): Bool**

- cultureAccessor defaults to the culture defined in settings
- ignoreCase defaults to false

Sample::

  String word = "apples";
  Bool endsWithLowercaseS = String.EndsWith(word, "s");
  Bool endsWithAnyS = String.EndsWith(word, "s", true);


String.IndexOf
---------------
Finds the zero-based starting index in the input string of the given substring searchString, provided the substring is part of the input string. If searchString is String.Empty, returns 0. If searchString is not in inputString, returns -1.

Overloads
~~~~~~~~~
1. **String.IndexOf(String inputString, String searchString, Bool ignoreCase, ICultureAccessor cultureAccessor): Int**
2. **String.IndexOf(String inputString, String searchString, Bool ignoreCase): Int**
3. **String.IndexOf(String inputString, String searchString): Int**

- cultureAccessor defaults to the culture defined in settings
- ignoreCase defaults to false


Sample::

  String word = "apples";
  Int32 whereIsL = String.IndexOf(word, "l");

String.Length
-------------
Returns the length of a string as an integer.

Overloads
~~~~~~~~~
1. **String.Length(String str): Int**

Sample::

  String.Length("word") == 4;

String.LengthBetween
--------------------
Returns true if string is between a specified minLength and maxLength range, otherwise false. Can specify inclusive or exclusive range.

Overloads
~~~~~~~~~
1. String.LengthBetween(String str, Int minLength, Int maxLength, Bool inclusive): Int**
2. String.LengthBetween(String str, Int minLength, Int maxLength): Int**

- inclusive defaults to false
- str cannot be null
- minLength must be greater than or equal to 0
- maxLength must be strictly greater than 0
- maxLength must be strictly greater than minLength
- if inclusive is false, returns true if str length is strictly greater than minLength and strictly less than maxLength
- if inclusive is true, returns true if str length is greater than or equal to minLength and greater than or equal to maxLength

Sample::

  record -> 'Name' : record['FirstName'] <- String.LengthBetween(record['FirstName'] to String, 2, 10), 'Sir/Madam'

String.IsEmpty
--------------
Returns true if input string is empty, otherwise false.

Overloads
~~~~~~~~~
1. **String.Empty(String str): Bool**

Sample::

  String.IsEmpty("") == true;
  String.IsEmpty(String.Empty) == true;
  String.IsEmpty("string") == false;

String.IsNullOrEmpty
--------------------
Returns true if input string is null or empty, otherwise false.

Overloads
~~~~~~~~~
1. **String.IsNullOrEmpty(String str): Bool**

Sample::

  String.IsNullOrEmpty(null) == true;
  String.IsNullOrEmpty("") == true;
  String.IsNullOrEmpty(String.Empty) == true;
  String.IsNullOrEmpty("string") == false;

String.IsNullOrWhiteSpace
-------------------------
Returns true if input string is null or entirely whitespace, otherwise false.

Overloads
~~~~~~~~~
1. **String.IsNullOrWhitespace(String str): Bool**

Sample::

  String.IsNullOrWhitespace(null) == true;
  String.IsNullOrWhitespace("        ") == true;
  String.IsNullOrWhitespace("This is a sentence") == false;

String.Repeater
---------------
Takes a header, two lambda arguments repeated one after the other (alternating) records.Count() times, and a footer, concatenates them together and returns the resulting string.

Overloads
~~~~~~~~~
1. **String.Repeater(Record[] records, String header, LambdaArgument arg1, LambdaArgument arg2, String separator, String footer): String**

Sample::

  ForEach(records, record -> {

      Record[] clientRecords = dataRecords;

      String headerTemplate = @"<table style='width:450px; border: 1px solid grey' cellpadding=0 cellspacing=0>
        <tr>
            <th style='border: 1px solid #c8c8c8;text-align:left;padding-left:10px'><font face='verdana'><font size ='2'>Invoice Date</th>
            <th style='border: 1px solid #c8c8c8;text-align:left;padding-left:10px'><font face='verdana'><font size ='2'>Invoice Number</th>
            <th style='border: 1px solid #c8c8c8;text-align:left;padding-left:10px'><font face='verdana'><font size ='2'>Amount Due</th>
        </tr>";
      String invoiceDataHtml = String.Repeater(clientRecords, headerTemplate,
        y -> @"<tr>
            <td style='border: 1px solid #c8c8c8;padding-left:10px'><font face='verdana'><font size ='2'>#{y.InvoiceDate}</td>
            <td style='border: 1px solid #c8c8c8;padding-left:10px'><font face='verdana'><font size ='2'>#{y.InvoiceNumber}</td>
            <td style='border: 1px solid #c8c8c8;padding-left:10px'><font face='verdana'><font size ='2'>#{y.AmountText}</td>
        </tr>",
        y -> @"<tr>
            <td style='border: 1px solid #c8c8c8;padding-left:10px'><font face='verdana'><font size ='2'>#{y.InvoiceDate}</td>
            <td style='border: 1px solid #c8c8c8;padding-left:10px'><font face='verdana'><font size ='2'>#{y.InvoiceNumber}</td>
            <td style='border: 1px solid #c8c8c8;padding-left:10px'><font face='verdana'><font size ='2'>#{y.AmountText}</td>
        </tr>",
        y -> String.Empty,
        '</table>'    
      );

String.Replace
--------------
Searches the input string str for instances of the substring searchString, and replaces all of them with replacementString.

Overloads
~~~~~~~~~
1. **String.Replace(String str, String searchString, String replacementString): String**

- None of str, searchString, and replacementString can be null
- searchString cannot be an empty string

Sample::

  String.Replace("I am very calm right now", "very calm", "nearly s****ing myself");

String.Split
------------
Returns a string array containing substrings of the original string delimeted by specified delimeter.

Overloads
~~~~~~~~~
1. **String.Split(String str, String delimeter): String[]**

- str cannot be null

Sample::

  String[] stringArr = String.Split("This is a sentence.", " ");
  stringArr[0] == "This";
  stringArr[1] == "is";
  stringArr[2] == "a";

String.StartsWith
------------------
Returns true if the search string begins with the input string, otherwise returns false. If ignore case is set to true, then case differences are disregarded when comparing the strings.

Overloads
~~~~~~~~~
1. **String.StartsWith(String inputString, String searchString, Bool ignoreCase, ICultureAccessor cultureAccessor): Bool**
2. **String.StartsWith(String inputString, String searchString, Bool ignoreCase): Bool**
3. **String.StartsWith(String inputString, String searchString): Bool**

- cultureAccessor defaults to the culture defined in settings
- ignoreCase defaults to false

Sample::

  String word = "apples";
  Bool startsWithLowercaseA = String.StartsWith(word, "a");
  Bool startsWithAnyA = String.StartsWith(word, "a", true);

String.ToLower
--------------
Converts a STRING to all lowercase.

Overloads
~~~~~~~~~
1. **String.ToLower(String str, ICultureAccessor cultureAccessor): String**
2. **String.ToLower(String str): String**

- cultureAccessor defaults to the culture defined in settings
- throws an exception if str is null

Sample::
  String.ToLower("WORD") == "word";

String.ToProper
---------------
Converts a string to proper casing, i.e. converts first letter of each word to uppercase.

Overloads
~~~~~~~~~
1. **String.ToProper(String str, ICultureAccessor cultureAccessor): String**
2. **String.ToProper(String str): String**

- cultureAccessor defaults to the culture defined in settings
- throws an exception if str is null

Sample::

  String.ToProper("mrs anderson") == "Mrs Anderson";

String.ToUpper
--------------
Converts a string to ALL UPPERCASE.

Overloads
~~~~~~~~~
1. **String.ToUpper(String str, ICultureAccessor cultureAccessor): String**
2. **String.ToUpper(String str): String**

- cultureAccessor defaults to the culture defined in settings
- throws an exception if str is null

Sample::

  String.ToUpper("word") == "WORD";

String.Trim
-----------
Removes all leading and trailing whitespace characters from a string.

Overloads
~~~~~~~~~~
1. **String.Trim(String str): String**

Sample::

  String.Trim("       space        ") == "space";