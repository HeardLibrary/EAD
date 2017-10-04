# The following commands use the Find and Replace tool in Atom to normalize dates at the Year level in EAD docs. The Regex option must be enabled. Performing these commands in the order listed will ensure that dates are not “fixed” twice/incorrectly.

## Find a YYYY-YYYY date range and normalize:
Find: <unitdate>(\d\d\d\d)-(\d\d\d\d)<
Replace: <unitdate normal="$1/$2" type="inclusive"><

## Find a YYYY-YYYY date range when months and/or other text is also present, and normalize the years:
Find: <unitdate>(.*(\d\d\d\d).+(\d\d\d\d).*)<
Replace: <unitdate normal="$2/$3" type="inclusive">$1<

## Fix inclusive dates from the same YYYY:
Find: <unitdate normal="(\d\d\d\d)/\1" type="inclusive"
Replace: <unitdate normal="$1"

## Find a single YYYY date and normalize:
Find: <unitdate>(\d\d\d\d)<
Replace: <unitdate normal="$1"><

## Find remaining single YYYY dates that include text and normalize:
Find: <unitdate>(.*(\d\d\d\d).*)<
Replace: <unitdate normal="$2">$1<
