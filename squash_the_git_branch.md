## Squash the git branch

I had close to 30 commits in my branch and I wanted to squash it all. `git rebase main -i` was not an option to me since I had many merge commits for which I had done resolution, and going thorough was a pin I didn't want to inflict myself.

I found this command: `git reset $(git merge-base main $(git branch --show-current))` which allows me to reset those files that don't match the main branch.
With this I was able to remove the older commits, successfully commit all the changes into a single commit. The only downside of this is, I have to do a force push on the branch.
