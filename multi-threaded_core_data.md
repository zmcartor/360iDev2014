#Multi-threaded Core Data

Don't ever block the main thread, of course!

Move parsing and saving onto a background queue. This is first step to a really great stack.

Create a new queue with privateQueuConcurrencyType. 

``` 
let context = NSManagedObjectContext(concurrencyType:privateQueueBlah)

context.performBlock(){
context.persistentStoreCoordinator = ourPersistentStoreCoord
	... do block operations
	}
```

The context with private concurrency will perform async operations within the block. Nice.


### Two PersistentStoreCoordinators

When data is either written or read, the NSpersistentStoreCoordinator is locked. In our current stack, a background queue is writing data and performing parsing within the ```performAction()``` block; but the UI also needs to read data for the UI. The UI has to wait for writing to stop, Darn :/

Create a coordinator for reading and another for writing. Now the locks will not interfere with each other.

Write-ahead-logging (WAL) - this is a SQLite feature will allows reading and writing to happen at once. Reading doesn't actually 'read' the new pages of data until they are actually committed. In iOS7, this is automatically turned on.

### Update the MainContext with changes

The data writer will need to pass those changes up to the MainContext. This is easy with 'mergeChangesFromContextDidSaveNotification:'However on a very very huge save , merging all these changes can block stuff up. Not good! To fix this, batch import the changes in groups of N.

Also, re-fetching data on a context causes it to goto disk and update any objects within the context. When to re-fetch can be done with custom-notifications or completion blocks.

Custom cells with different heights can really mess stuff up. Batched saves can help here.

### Avoiding Merge Conflicts
The best way is to create a single writer queue. Each operation dispatches onto this writer queue. This way writes aren't happening at the same time and potentially modifying the same bit of data. Let SQL handle the concurreny for you.

There's also the option of parent/child contexts. Either is not theoretically faster than the other, but parent/child is tougher to get right (says the speaker.)


##Keep the main thread read only!

