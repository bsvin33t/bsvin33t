# [Flag shih tzu](https://github.com/pboling/flag_shih_tzu) with [Papertrail](https://github.com/paper-trail-gem/paper_trail)

In my organization, we use both flag_shih_tzu to manage preferences on our customer objects and we track the changes using papertrail.

A request came from the product team that they wanted to see what changed.

For this, my initial solution was that we just create some kind of mapper between the external preferences representation and the internal flags.

As of now, we use flags to manage only 2 (email) preferences. If we add one more, then the number of states that need naming will be multiplied by 2. This will pose a challenge, and this was not very useful either, as the requirement was to give a list of preferences that were true/false and what they changed to.

We ended up with a solution where we just passed the old flags(from papertrail) to an object that is not persisted, compare it with the existing preferences, then return the result. I liked the approach. We haven't implemented the solution. Once we do, I will consider updating this post with code samples.

Please feel free to raise an issue if you felt this post needs more information.

Cheers

Vineeth
