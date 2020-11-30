Category:: [[SSB]]


I really like the layout and style of the SSB protocol guide: [https://ssbc.github.io/scuttlebutt-protocol-guide/](https://ssbc.github.io/scuttlebutt-protocol-guide/) I can't find the source anywhere. I guess it's hosted on the scuttlebutt network? 

So it uses a RPC protocol for requesting things from peers. You call a function on your peers server and then it responds with the results of that function. 

Requests are sent with a request number, and then the peer sends back the negative of that request number as the response request number. The request number is a signed number so can be negative. By utilizing the negative sign in this way clients know when the peer is responding to one of their previous requests vs making it's own request to them. 

**createHistoryStream is how you request a feed from another peer with all their messages / posts etc**. It is called with the following request:

```
[{
	name: ["createHistoryStream"],
	type: "source",
	args: [{"id":"<feed id>"}]
}]
```

The "type" being set to source means to stream all the data back, so there will be more than one response coming back to the client which it should wait for. When the server is done sending data for this request it sends a message with the body type of JSON, and end/err of "true" and a body of just "true", saying that it closed successfully. 

To request some certain blobs of data from someone you can use the request "blobs" "has". So it looks like the followign:

```
[{
	name: ["blobs", "has"]
	type: "async"
	args: ["<blobId>"]
}]
```

So the args is an array of all blobs we are requesting. The async type means only one response is sent rather than a whole bunch like the createHistoryStream request above. 

It looks like the name and args fields are always arrays, and type is a string. 

## Feed Messages

Here's an example message:

{
```
{
 	"previous": "%XphMUkWQtomKjXQvFGfsGYpt69sgEY7Y4Vou9cEuJho=.sha256", 
	"author": "@FCX/tsDLpubCPKKfIrw4gc+SQkHcaD17s7GI6i/ziWY=.ed25519", 
	"sequence": 2, 
	"timestamp": 1514517078157, 
	"hash": "sha256", 
	"content": { 
		"type": "post", 
		"text": "Second post!" 
	}, 
	"signature": "z7W1ERg9UYZjNfE72ZwEuJF79khG+eOHWFp6iF+KLuSrw8Lqa6 IousK4cCn9T5qFa8E14GVek4cAMmMbjqDnAg==.sig.ed25519" 
}
```

So it looks like every message contains the public key of the author, and a signature showing it was signed with the private key belonging to that public key. This means that feeds could contain posts from multiple public keys it seems, so you could have other authors in your feed. That doesn't make sense to me, why would they do that? Or is it just that the public key is added every time for security reasons somehow? I don't know why the public key can't just be specified in the content of the very first message and then this feed is tied to this key forever. 

The reason there are two timestamps in the response from createHistoryStream is the one inside the message is when the message was posted, while the one inside the response from createHistoryStream is the time that this peer received this message. 

## Blobs 

### getSlice

So you can request just a slice of a blob of data, this is really cool for being able to download data from many peers at once, just request a slice of it from lots of people and if any requests time out then get those slices from others. This way you can develop a full peer to peer streaming mesh where everyoen can download from everyone else at maximum speed. This is cool!

###  createWants 

Is a message saying "hey what blobs do you want?" to your friends, and they can then return blobs they are seeking, or blobs that their friends are seeking. 

The other person can say they want the blob by returning the blob hash with a negative number where -1 is they want it, -2 is their friend wants it, -3 is some other peer wants it. The other person can say they have a blob by sending a positive number of the number of bytes in the blob. 

## Invites

The command "Invite", "use" is a command to use an invite to get a pub to follow you back. For some reason it doesn't include the invite code in the request which is weird. Oh maybe it's because invites are created with a new private key from the pub server and so when you use the invite you first connect to that private key that was just created, so the server knows you're making a request against that new invite key. 

Oh yea so you handshake with the private key and then the pub server knows you're trying to use the invite associated with that key.
