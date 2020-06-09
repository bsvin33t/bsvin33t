Imagine this, `comments` AR object needs to be associated with `service_provider`, `consumers` and `unregistered_users`.

The "Rails" way to do it is to go with something like a `comments` table, 
have a polymorphic association between the rest of the objects and be done with it.

This doesn't really provide us with the safety of having forigin keys. 
Still what would be another reason to split it up into multiple tables?

It is, the fact that we fetch all the comment records scoped to a specific user when we get it, makes us sure to have it in
multiple tables.

This way, we get the safety of having forigin keys from the DB.
