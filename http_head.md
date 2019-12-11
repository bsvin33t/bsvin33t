# HTTP HEAD

We wanted to move away from storing URLs as strings to using [shrine](https://github.com/shrinerb/shrine).

For this, once the file has been uploaded from the presigned endpoint, 
we wanted to fetch the metadata in a callback, and create associated records.

To fetch the metadata, all I had to do was use [Faraday](https://github.com/lostisland/faraday)'s nice head method.

Mind blown.

Please feel free to raise an issue if you felt this post needs more information.

Cheers

Vineeth
