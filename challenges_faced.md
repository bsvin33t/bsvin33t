# Challenges faced

Life as a SWE is not too easy. Systems are complex, here are some things that I encounter on a daily basis.

I introduced a bug in the system when we were migrating from minions to sp-admin, at that time,
I introduced a bug that closed close to 150K enquiries.

How did I solve it?

We informed the operations/customer support team about this.
I and my team lead started to look at all the affected enquiries.
We changed the settings that were being picked up.
We found them out by looking at the updated at timestamp, along with the closed enquiries.
Since this is just a state transition, I wrote a rake task that updates the enquiries to the actual state, 
this was simple since we do record level tracking using audit trails.

There was a 3rd party system that we pushed our updates to, 
we got the information from their team a little later when we tried to close the enquiries that were already "closed" and reopened.

The result of this mishap was that we started to take a look at the default configuration that were set for our apps, 
how env vars are being used in our app, and eleminate duplicates and overrides, and just have ansible do the management of constants like these.

There was another time when I pushed an update, and that update had a bug where the layout of the documents that were supposed to sent to pingen was incorrect.
This caused us(my operations team) to receive the backlog of paper mails to be sent, where they had to print out each email, fold it in and post it. It was not a good feeling.

Missed deadline due to crappy communications and timezone issues with the 3rd party provider, which caused wasted effort on marketing.


And then, there are these everyday problems/debugging tasks where we expect something has to be created/updated but due to an error from the system, 
it wouldn't have happened, execptions would have been swallowed because of the way we would have handled errors, which are discovered by logs.

Also, silly and stupid things like, 
opening a file in every instance of the rails process causing memory bloat, which caused the monitoring system to scream at us.

There is another instance where the client uploads data that is corrupted and blames us/our team for it.

Feature toggle was supposed to be turned on, it was not. The business assumed that it was turned on and started to use it(send out email). We had to manually trigger those emails. I don't really know if there is a good solution for that.

Email validations. We ran a rake task that updated the email addresses of a bunch of our users to not contain special characters in the email. This had unintended consequence of users who had not registered in our service receiving emails.

When sending out emails(or doing async stuff) inside async stuff, make sure that there is no points of failure after the sending out of email, if there are cases of exceptions, then make sure that the scheduling of emails is skipped. We ended up sending some 7 emails for 2 customers each because of this.
Summarizing, if you schedule a job inside a job, then the inner job should be the last thing that the outer job should execute.

Working with emails of weird encodings. We check the encoding on the emails, if the encoding is not present on the email headers, then we try to encode it in UTF-8.
If that is not possible, we encode in `ISO_8859_15`. 

Communication when delegation. What my vision is for the execution, how the project is executed, comes down to communication of details that are captured within.

I came to discover the `store :parameters` in AR is not storing the data in the JSONB format, as the column defines, instead, stores it as a string(and thus unqueryable).
I have to ensure that the data that is written to the db/persistent is what I expect it to be.

Our team is the maintains and builds the "core" of the business. 
As of now we are exposing our api endpoints as graphql mutations and queries, instead of using REST apis.

We ended up with this because there was frequest change requests on our API whenever some new function was needed.
This caused us to spend more and more time on writing and re-writing, versioning our controller and serializer logic, 
instead of focusing on adding more value to the business by building business features instead of plumbing.

Now that we experienced this kind of misery, grqphql was a breath of fresh air. 
We have middleware apps that expose themselves to the client apps as rest APIs that consume the grqphql APIs.
This has given us more and more confidence with introducing changes into our system. 
We also have a dedicated middleware team that ensures that appropriate data is being exposed to the clients according to their needs.

A day ago, I changed the way a public facing API worked as it had to work a little differently for internal use.
I, instead of duplicating the code, reused it with a bit of extension, that was incompatible. 
This caused problems for the users, they were unable to create matches.
I discussed this with my team lead, we came to the conclusion that, when external facing APIs are to be used internally, even if they are similar, we will create a different one. Duplication is ok. The users of the APIs have to be informed about the change.

A day ago, we had our backoffice app crashing. We figured the reason. It was because of the degraded service provided by S3.
Why was this an issue? We were downloading an email file from S3 to show the subject in our api.
With the degraded S3, the downloads were slower and the entire thing to time out was taking some 60 seconds.
This caused the requests to be queued up and eventually, brought our system to its knees.
How did we fix this? We just went and changed the NGINX configuration to time out at 30 seconds, as we didn't want to muddy our codebase with a timeout block.
