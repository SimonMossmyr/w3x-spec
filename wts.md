# "war3map.wts" The trigger string data file

Open it with notepad and you'll figure out how it works. 

Each trigger string is defined by a number (trigger ID) and a value for this number. When Warcraft meets a "TRIGSTR_***" (where "***" is supposed to be a number), it will look in the trigger string table to find the corresponding string and replace the trigger string by that value. The value for a specific trigger ID is set only once by the first definition encountered for this ID: if you have two times the trigger string 0 defined, only the first one will count. The number following "STRING " must be positive: any negative number will be ignored. If text follows "STRING ", it'll be considered as number 0.

String definition:

It always start with "STRING " followed by the trigger string ID number which is supposed to be different for each trigger string. Then "{" indicates the begining of the string value followed by a string which can contain several lines and "}" that indicates the end of the trigger string definition.

Example:

in the .WTS file you have:

```
STRING 0
{
Blah blah blah...
}
```

Then either in the .J, in the .W3I or in one of the object editor files, Warcraft finds a TRIGSTR_000, it'll look in the table for
trigger string number 0 and it'll find that the value to use is "Blah blah blah" instead of "TRIGSTR_000".
If there are more than 999 strings another the reference simply becomes one character longer.
