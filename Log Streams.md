Category:: [[SSB]]
Description:: An overview of the different stream/log names in SSB. 


`createHistoryStream` - Tries to create the full log of one SSB ID/user

`createUserStream` - This seems to be the same as createHistoryStream. 

 `createFeedStream` is the same as `ssb-server feed` which is all messages in all feeds ordered by message publish time. This is the timestamp the author chose, so could be made up. Default order is incrementing chronological, can use `--reverse` to see most recent messages first. 
 
`createLogStream` is the same as `ssb-server log` which gets all items from all feeds ordered by receive time. This is the local receive time of the server. Default order is incrementing chronological, can use `--reverse` to see most recently received messages first. 


## Viewing live log of incoming messages

```
ssb-server log --reverse --live --gt $(date +%s%N | cut -b1-13)
```

Without the `--gt` it prints the entire stream first then listens for more.


