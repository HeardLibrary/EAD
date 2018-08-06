# University Archives Finding Aids

This folder includes finding aids downloaded into XML format from a Microsoft Access database as well as finding aids that have been converted for ingest into ArchivesSpace.

## Fixing records from initial download

1. Perform these find and replace regexes to fix records from their initial downloaded state.

Find:
```
<(.*)>\s*<Folder_x0020_Name>(.*)</Folder_x0020_Name>\s*<Box_x0020__x0023_>(.*)</Box_x0020__x0023_>\s*<Folder_x0020__x0023_>(.*)</Folder_x0020__x0023_>\s*<Date_x0020_Begin>(.*)</Date_x0020_Begin>\s*<Date_x0020_End>(.*)</Date_x0020_End>\s*<RG>(.*)</RG>\s*</\1>
```

Replace:
```
<c01 level="file"><did><unittitle>$2</unittitle><unitdate>$5-$6</unitdate><container type="box">$3</container><container type="folder">$4</container></did></c01>
```

2. Pull the info from the template.xml and insert the c01 tagged items between the <dsc> tags

3. Perform date normalization regexes

4. Fix anomalous items

5. Ingest into ArchivesSpace
