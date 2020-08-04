### Git history

I was running specs on `sp-web` and it started to fail because its dependency, `sp-persistence`, had a class missing.
I wanted to check what happened to it and found it was deleted.

I wanted more, I wanted when it was delted, and why it was deleted.

`git log --full-history  -- myfile` helped me out. I was able to figure out which commit delted it and why it was deleted.
