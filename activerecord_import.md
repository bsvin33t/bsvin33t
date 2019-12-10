# Activerecord import is a very useful gem.

The feature is already present in Rails 6 now.

One of the APIs that I was using sent back close to half a million records(ofcourse it was paginated).

I had to import this into our database with the upsert action. For this initially I did `find_or_create`.

So slow.....

I was considering to build an SQL query using the JSON that arrived.

Woe is me!

This is not the way to import bulk data, told my co-worker.

He pointed me to (activerecord_import)[https://github.com/zdennis/activerecord-import]

BAM! 15 mins later, all all the data that was out there in the API is in my DB.


Please feel free to raise an issue if you felt this post needs more information.

Cheers

Vineeth
