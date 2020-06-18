Too many a posts have been written where side effects were shown shade. Here is another from me to the many.

Recently, I was travelling back from Bangalore to Berlin, I get this slack message from TL.
I was inserting records into the DB, but I was not triggering the relvant activerecord callbacks, 
as I was just doing a bulk insert in a single SQL statement.

The side-effect that I hate is the activerecord callback. 
The thought that I have is, should the part of the application be written as a pull based model?
(where the other class/job figures out what all changed and runs some code based on that)

If it is changed to a pull based model, how will the architecture change?
