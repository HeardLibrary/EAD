# Working EAD Documents
This document details the EAD finding aids that are unable to be imported into ArchivesSpace in their current form. Where available, it also contains the issues that each individual xml doc has and what steps need to be taken to repair. As documents are repaired, they will be removed from this list and added to the Finalized EAD folder.

## FinneyClaude (MSS.0140)
There is already another Claude Finney collection in ArchivesSpace (MSS.0139). This appears to be a set of documents (now in xml) listing Keats objects held by other institutions. Most of these documents turned out to be photocopies and were deaccessioned. The rest were integrated into MSS.0139. This collection (MSS.0140) no longer exists.

## LawsonJames (MSS.0626)
This collection is currently in the middle of processing. This finding aid was produced from an early 2017 version of the inventory, but it is still unclear if this is the current structure. Work has been paused on this project until the status can be determined, or until the collection is fully processed.

## RiceGrantland (MSS.0364)
Gives an error of
```
Error: #&lt;Sequel::DatabaseError: Java::ComMysqlJdbc::MysqlDataTruncation: Data truncation: Data too long for column &#39;value&#39; at row 1&gt;
```

## SilbermanLou (MSS.0392)
This collection is broken into a subject table, article table, and correspondence index. It will need some regexes performed on it but can then be easily added to the existing ArchivesSpace record.

## VannElizabeth (MSS.0476)

## WillsJesse (MSS.0001)
This collection has some issues that can be fixed with Xquery. This includes pulling titles and box/folder info from single <unittitle> fields. There may be other issues with it.
