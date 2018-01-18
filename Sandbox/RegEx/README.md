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
