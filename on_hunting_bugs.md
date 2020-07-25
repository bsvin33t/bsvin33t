I and a colleague(Tony) were looking for a bug where we were told by the users that once they uploaded the file,
and then downloaded it, the file was corrupted.

We spent some time trying to figure out what was going wrong. We maded quite a number of hypothesis, one where S3 was messing the file, among others.

Then, we started to find what was the fault. 
The way our upload works is, first we generate a presigned endpoint from our app for S3. We give that to the front-end client. 
The front-end client uploads the file there and S3 returns back a URL to the client where the file is living. 
Once this happens, the front-end client posts the URL to our app. We then promote the file from the "cache" to "storage"(look at shrine for more details).

We then started to trace the journey of the file. We decided to "skip" the part where we get the front-end client to upload the file,
instead we got shrine to do the promotion. Then we downloaded the file from S3. We saw that the file was intact,
which got us to conclude that the front-end client was messing the upload. And it was no fault of S3 or shrine's "promote". 

This happened on the Friday, I'm writing the blogpost on Sunday. We are going to have a conversation with the front-end team on Monday.

Cheers!
Vineeth
