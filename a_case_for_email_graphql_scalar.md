### A case for email scalar in graphql.

Check out the docs here: https://graphql-ruby.org/type_definitions/scalars

Does it make sense to add email as a graphql scalar? We have URL as a scalar, so why not email?

One reason why I think we don’t need it is because, unlike DateTime, we don’t need to translate it to a “ruby” object.

But then, we want to ensure the email follows a certain format.
This way, we can also indicate to the clients that the data that they are going to receive is going to be of a certain format(type). 
And I think they can build stuff more easily with this info; 
It also indicates to the clients that there will be a certain kind of input validation on the type side.
