Scuttlebutt uses [muxrpc](https://github.com/ssbc/muxrpc) for talking between client and server. This is what allows the client to be a separate app that communicates to the server API's that are exposed by each plugin. 

To make an RPC request, send a JSON message containing the name of the procedure to cal. 

You can call the RPC procedure createHIstoryStream to get a stream of a log of another person. I believe this can be called on remote instances of SSB. 

It's really quick for messages to get from my PC to a pub. Just tried following my test user by running this on the us-west server. 

```
 ./sbot createHistoryStream --id "@Cq6uh+PrO2BFZuEXZkGMzTeDPbbcFRwhHrq7UjLiQzg=.ed25519" --live
```

And after posting in patchwork it appeared in <1s on ssb peernet us-west