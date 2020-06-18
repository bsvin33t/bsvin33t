It is always possible that the current branch is stale compared to the branch in the remote.
Today, I spent some good 10 to 15 mins scratching my head to figure out why my colleague's env var change was not present.
Then, I had the idea of checking if the branch was merged, which made me realize that I was working on a stale branch.

I pulled the latest code and voila, the changes are on my machine.
