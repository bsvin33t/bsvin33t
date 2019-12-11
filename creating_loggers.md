# Creating Loggers.

I caused a memory leak in our system by not initializing the loggers in the `/initializers` directory.

This causes an instance of logger to be created everytime a request arrives at the server, which in really un-necessary.

I want to read up on how other frameworks handle this.

Please feel free to raise an issue if you felt this post needs more information.

Cheers

Vineeth
