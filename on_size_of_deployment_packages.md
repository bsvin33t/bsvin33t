### On the size of the deployment package.


We were building our rails deployment package to include the git. This allowed us to track what was deployed.
And then, we started to realize that our deployment size was getting really out of hand and wanted to shrink it down.

TADA-- git's shallow clone.

`git clone --depth 1 https://url.git`
