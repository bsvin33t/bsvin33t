ZSH aliases.

Pretty useful.

Created an alias for me that lists the changed spec files.

I'm still yet to find out how to give this as input to rspec so that one command, and I will have all my changed specs running.

`git status | grep spec | cut -c 14- | sort -t: -u -k1,1 | tr '\n' ' '`
