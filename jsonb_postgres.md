# Working with JSONB and POSTGRES database

I was faced with a problem today. We are using AWS S3 to upload, store files, in conjunction with shrine.

But when we built the feature, we didn't start to use shrine,
instead just uploading the file and storing the return values as an array in JSON column on PG.

For testing purposes, we ended up having some rubbish data on our staging DB.
These rubbish URLs don't point to S3, instead to different sources.

I had to write an Activerecord query with supoprt to JSON to fetch them.

For that I wrote the following:

`DB::Questionnaires::ConsumerMediaQuestionAnswer.where.not("value ->> 'media_urls' like '%https://ours3-staging.s3.eu-central-1.amazonaws.com%'")`

Pretty cool stuff from Postgres. I knew how to get data from the JSONB field, but I didn't know the syntax to query it.

I just googled `using like on json fields + postgres`

To write the query, I used this SO post: https://stackoverflow.com/questions/42918348/postgresql-json-like-query

Please feel free to raise an issue if you felt this post needs more information.

Cheers

Vineeth
