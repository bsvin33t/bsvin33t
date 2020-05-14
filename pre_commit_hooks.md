I wanted to speed my rubocop up. Rubocop takes close to 25s to start and execute in my machine.
I was also missing running the schema update of my graphql. Here is the small pre_commit hook command that I run.

```
#!/usr/bin/env bash
git diff --diff-filter=d --cached --name-only | grep -E '\.(rb)$' | xargs bundle exec rubocop -P
git diff --cached --name-only | if grep --quiet "app/graphql/queries/\|app/graphql/mutations/"
then
  bin/rake graphql:schema:idl;
fi
```
