#Offline is not special case

Update the UI unobtrusively. Use fetchedResultsController, or KVO.

When user wants to see a screen, fetch the data from DB. Attempt to fetch data from network. If this succeeds, cool. Update the UI via KVO. If not, don't do anything. Failure is a failure. 

### Maintain a local cache, of course
Maintain a local cache and keep as fresh as you need. Fetch new data in the background only when needed. Update unobtrusively. Notify user if new data is not yet available if need be. This depends on nature of the datas.

Within the local data model, use a sync-flag to keep track of whether a change has been synced, needs sync, or whatever. 

### Queue Up

If the network is down, queue up operations which require data sync or some other type of op. Make sure to persist these changes to disk so the queue can be re-played when the app is closed. ```NSURLRequest``` conforms to NSCoding, so this is an option.  Create some NSOperations and put them in a queue.


### Background fetch
Periodically launch in the background to catch up with the server, or replay various queue operations. (is background fetch one way??)


### Reachability 

If packets are able to really leave the device, then reachability will show as 'connected.' However network operations will eventually time out. To get around this, show a dialog like "its taking a long time to send this X" and then attempt to send it later via Queue, or create the notion of a 'drafts' area if appropriate. 

### Use UUIDs
Maintain a UUID for a piece of data, so it can be tracked, expired, or updated with a unique identifier. 



