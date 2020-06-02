Polymorphic association, or tagged association; Causes pain. How does it cause pain you ask?

We won't be able to have forigin key, this in turn causes data integrity problems.

Here is an example:

We have `complaints` that can be associated with `service_providers` OR `consumers`,
we decided, we can go with polymorphic association here, calling it `complained_by`.

Then, we eneded up deleting(rather soft deleting)  a consumer, with whom a complaint was associated.
We then tried to fetch the complaint data and associated users in a promise(GraphQL),
the promise started to fail when it was being resolved.

After some head scratching, we figured out that the associated user was missing, 
but the complaint table was not updated with it.

This makes me feel that even though polymorphic association is nice, I think having separate table, 
with good forigin keys would have solved this issue

Further reading: https://stackoverflow.com/questions/922184
