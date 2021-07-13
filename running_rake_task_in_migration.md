# Running rake task in migration

### Here is a conversation that I saw in one of the slack channels.

M S Today at 10:40 AM
i am running a rake task through a migration but migration still down even after it is run. Should n’t it be up?
10 replies

Florian Dutey  6 hours ago
you shouldn’t call rake tasks from migrations. Just migrate your structure

Florian Dutey  6 hours ago
migrations are transactionnal, if your rake task is performing a lot of updates, it’s gonna lock the db for very long time and eventually your whole server will go down

M S  6 hours ago
Yeah. I know that but I still need it and it’s not lot of updates. What I am not sure about is, shouldn’t the migration be up after running rake task?

Tobias  6 hours ago
if it's not a lot, why not do it in the migration?

Florian Dutey  6 hours ago
if it’s not a lot, why not do it in the migration?
Do it in the migration directly, preferably through raw SQL. Migratons are low level, like any object, they should not call higher level objects to run (and rake task is on the highest level possible) (edited) 

Florian Dutey  5 hours ago
The easiest solution is to
create a job to migrate your data and define a proper schedule strategy (according to some batching strategies, you don’t migrate millions of records like you migrate couple of them)
run migrations
deploy the new code
deployment will reset your scheduler and data migration will be ran in the background. This way you can monitor the data / errors and your whole stack (including the db) is not stuck in a fucked up state because the migration went sideway
BTW, postgresql migrations are transactionnal but last time i checked (might have changed since then), mysql ones were not (mysql doesn’t / didn’t support transaction on table structure changes).
So with mysql (if it’s still the case), if your migration fails after changing the structure because your task / data migration fails, you’re a deep trouble. The migration tag is not added into the db (as it’s added last) but the structure changed. Since your deployment failed you will have to restart, it’s gonna try to apply the changes again and…. it’s gonna fail (edited) 

Florian Dutey  5 hours ago
keep thing separated and atomic as most as possible. Rule of thumb for everything

M S  5 hours ago
I got your point but my question is still same, why migration status is still same, i.e. down?

Florian Dutey  5 hours ago
i dont know, try to run them without the rake task and see if it’s the reason
