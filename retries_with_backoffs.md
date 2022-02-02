Recently when we were trying to get stats from elasticsearch, we started to see an error. 
A timeout error, to be more precise. The endpoint that was timing out was `"#{index_name}/_count"`. 
We were trying to get the count immediatly as our dataflow job finished processing and sending data into the index. 

The same endpoint was not causing any timeouts only a few moments later.
To fix the timeout, we used a nice little idea of doing a retry with exponential backoff.
The advantage of adding exponential backoff is that we get to retry, and if there is a failure, it adds an extra delay to it, so as to not overwehlm the downstream system\
(elasticsearch in this case, but probably this wouldn't have overwhelmed it.)

I ended up using the gem  (Retriable)[https://github.com/kamui/retriable], with the number of tries being 3 and a retry interval of 5 seconds, which ended up working just fine.
And thus we solved this issue.
