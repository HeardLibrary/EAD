# RegEx's

This folder includes multiple regular expressions (regexes) that can be used on xml documents. Also included are some test xml documents to use them on.

## Miscellaneous regexes

### Find <c0#> elements that incorrectly contain containers tags but no unitdates or unittitles:
```
<did>\s*<container .*>.*</container>\s*<container .*>.*</container>\s*</did>
```
The \s* look for in infinite amount of whitespace between the >< elements. If it encounters something besides whitespace (which would usually be a unittitle or unitdate), it won’t highlight.

## Normalizing Dates
The following commands use the Find and Replace tool in Atom to normalize dates at the Year level in EAD docs. The Regex option must be enabled. Performing these commands in the order listed will ensure that dates are not “fixed” twice/incorrectly.

### Find a YYYY-YYYY date range and normalize:

Find:
```
<unitdate>(\d\d\d\d)-(\d\d\d\d)<
```
Replace:
```
<unitdate normal="$1/$2" type="inclusive"><
```

### Find a YYYY-YYYY date range when months and/or other text is also present, and normalize the years:

Find:
```
<unitdate>(.*(\d\d\d\d).+(\d\d\d\d).*)<
```
Replace:
```
<unitdate normal="$2/$3" type="inclusive">$1<
```

### Fix inclusive dates from the same YYYY:

Find:
```
<unitdate normal="(\d\d\d\d)/\1" type="inclusive"
```
Replace:
```
<unitdate normal="$1"
```

### Find a single YYYY date and normalize:

Find:
```
<unitdate>(\d\d\d\d)<
```
Replace:
```
<unitdate normal="$1"><
```

### Find remaining single YYYY dates that include text and normalize:

Find:
```
<unitdate>(.*(\d\d\d\d).*)<
```
Replace:
```
<unitdate normal="$2">$1<
```

### Working formula to parse months:
This doesn’t currently work to do anything but Month xxxxx YYYY formatted dates. There would need to be a second F&R formula to change –Month into –MM format consistently.

Find:
```
<unitdate>((January|Jan|February|Feb|March|April|May|June|July|August|Aug|September|Sept|October|Oct|November|Nov|December|Dec).{0,6}(\d{4}).{0,30}(January|Jan|February|Feb|March|April|May|June|July|August|Aug|September|Sept|October|Oct|November|Nov|December|Dec).*(\d{4}).*)<
```
Replace:
```
<unitdate normal="$3-$2/$5-$4" type="inclusive">$1<
```

### Working formulas to parse months and days in Stahlman collection (MSS.0413)
This may or may not be useful for other collections. There would need to be a second F&R formula to change –Month into –MM format consistently.

Find single dates and normalize:
Find:
```
<unitdate normal=".*">((January|Jan|February|Feb|March|April|May|June|July|August|Aug|September|Sept|October|Oct|November|Nov|December|Dec).\s(\d{0,2}),\s(\d{4}))<
```
Replace:
```
<unitdate normal="$4-$2-$3">$1<
```

Find range of dates within same month and normalize:
Find:
```
<unitdate normal=".*">((January|Jan|February|Feb|March|April|May|June|July|August|Aug|September|Sept|October|Oct|November|Nov|December|Dec).\s(\d{0,2})\s{0,1}-\s{0,1}(\d{0,2}),\s(\d{4}))<
```
Replace:
```
<unitdate normal="$5-$2-$3/$5-$2-$4" type="inclusive">$1<
```

This is supposed to find a range of dates with different months and days and normalize. It is also detecting 'Month day - day, Year' results too, but I can't figure out why yet.
Find:
```
<unitdate normal=".*">((January|Jan|Jan.|February|Feb|Feb.|March|Mar|Mar.|April|Apr|Apr.|May|June|Jun||Jun.|July|Jul|Jul.|August|Aug|Aug.|September|Sept|Sept.|October|Oct|Oct.|November|Nov|Nov.|December|Dec|Dec.).\s(\d{0,2})\s{0,1}-\s{0,1}(January|Jan|Jan.|February|Feb|Feb.|March|Mar|Mar.|April|Apr|Apr.|May|June|Jun||Jun.|July|Jul|Jul.|August|Aug|Aug.|September|Sept|Sept.|October|Oct|Oct.|November|Nov|Nov.|December|Dec|Dec.)\s(\d{1,2}),\s{0,1}(\d{4}))<
```
Replace:
```
<unitdate normal="$6-$2-$3/$6-$4-$5" type="inclusive">$1<
```

Fix single days and add missing 0 in front of it:
Find:
```
"(\d{4}-\d{2})-(\d)"
```
Replace:
```
"$1-0$2"
```

Find range of dates within same month and normalize:
Find:
```
"(\d{4}-\d{2})-(\d)/(\d{4}-\d{2}-\d{2})" | "(\d{4}-\d{2})-(\d)/(\d{4}-\d{2})-(\d)"
```
Replace:
```
"$1-0$2/$3" | "$1-0$2/$3-0$4"
```

### Formula to remove tables from Dresslar (MSS.0120) Collections
Convert table1 to <c0#>
Find:
```
<row>\s*<entry colname="1">(.*)</entry>\s*<entry colname="2">(.*)</entry>\s*<entry colname="3">(.*)</entry>\s*<entry colname="4">(.*)</entry>\s*<entry colname="5">(.*)</entry>\s*<entry colname="6">(.*)</entry>\s*<entry colname="7">(.*)</entry>\s*</row>
```
Replace:
```
<c02 level="item"><did><unittitle>$1, by $3 ($4)</unittitle><unitdate>$2</unitdate><container type="box">$5</container><container type="folder">$6</container><note><p>$7</p></note></did></c02>
```

Convert Outgoing Correspondence table to <c02>
Find:
```
<row>\s*<entry colname="1">(.*)</entry>\s*<entry colname="2">(.*)</entry>\s*<entry colname="3">(.*)</entry>\s*</row>
```
Replace:
```
<c02 level="item"><did><unittitle>$1</unittitle><unitdate>$2</unitdate><container type="box">$3</container></did></c02>
```
