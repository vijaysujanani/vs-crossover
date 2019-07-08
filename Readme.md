# PostMortem/Root Cause Analysis of the AES EDI jira (AESEDI-53447 #465)

## Date
2019-08-07

## Authors
*vs*
*Ops Team*

## Status
Complete, resolved

## Summary
The customer data was not sent from AES EDI. The investigation showed that 
the file with the data was sent, but it did not get processed due to an issue with the AES CIS service.

## Impact
About 486,000 records were affected and the EDI to CIS monitoring service too.

## Root Causes
There was a network failure due to aws outage in the region. 

## Trigger
A large amount of files were not processed.

## Resolution
Reloading the *AES CIS* monitoring service allowed us to spot the missed records that were not discovered automatically. 

## Detection
Our customer create this Jira to alert us on this failure. *Please refer to (AESEDI-53447)*


## Action Items
| Action Item | Type | Owner | Bug |
| ----------- | ---- | ----- | --- |
| Enabling Cross region replication of files in s3 to avoid such incidents | prevent | LMP | **DONE** |
| Monitor the data ingesters and processors (ETL) | prevent | LMP | (Jira Issue No: AESCIS-38263)**TODO** |

## Lessons Learned
We have to add more monitoring plugins and modules to watch this critical part of our infrastructure. 

## Timeline

2018-10-24 (*all times UTC*)

| Time  | Description |
| ----- | ----------- |
| 11:56 | Discovering of the missing files |
| 12:00 | Restarting of the AES CIS monitoring module |
| 12:15 | Starting of the data processing of the records files |
| 13:00 | Completion of the data processing of all the 486,000 records files |
