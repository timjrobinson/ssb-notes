Category:: [[SSB Server]]

This is the manifest of ssb-server when no plugins are loaded:

```
{
	auth: 'async',
	address: 'sync',
	manifest: 'sync',
	multiserver: { 
		parse: 'sync', 
		address: 'sync' 
	},
	multiserverNet: {},
	get: 'async',
	createFeedStream: 'source',
	createLogStream: 'source',
	messagesByType: 'source',
	createHistoryStream: 'source',
	createUserStream: 'source',
	createWriteStream: 'sink',
	links: 'source',
	add: 'async',
	publish: 'async',
	getAddress: 'sync',
	getLatest: 'async',
	latest: 'source',
	latestSequence: 'async',
	whoami: 'sync',
	progress: 'sync',
	status: 'sync',
	getVectorClock: 'async',
	version: 'sync',
	help: 'sync',
	seq: 'async',
	usage: 'sync',
	clock: 'async'
}
```