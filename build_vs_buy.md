# Build V/S Buy

I was browsing HN and I came across this blogpost which was encouraging businesses to buy instead of build. I found this comment to be insightful.

One thing to pay close attention to when making a build v.s. buy decision is the impact that billing models will have on your usage of a tool.
Take logging for example. If you buy a log aggregation platform like Splunk Cloud or Loggly the pricing is likely based on the quantity of data you ingest per day.

This can set up a weird incentive. If you are already close to the limit of your plan, you'll find that engineers are discouraged from logging new things.

This can have a subtle effect on your culture. Engineers who don't want to get into a budgeting conversation will end up avoiding using key tools, and this can cost you a lot of money in terms of invisible lost productivity.

Tools that charge per-head have a similar problem: if your analytics tool charges per head, your junior engineers won't have access to this. This means you won't build a culture where engineers use analytics to help make decisions.

This is a very tricky dynamic. On the one hand it's clearly completely crazy to invest in building your own logging or analytics solutions - you should be spending engineering effort solving the problems that are unique to your company!

But on the other hand, there are significant, hard-to-measure hidden costs of vendors with billing mechanisms that affect your culture in negative ways.

I don't have a solution to this. It's just something I've encountered that makes the "build v.s. buy" decision a lot more subtle than it can first appear
