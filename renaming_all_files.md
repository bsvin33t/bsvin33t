An interesting question was posed before me today. How do I rename all files following a pattern inside my directory.

I was unable to come up with an artful one-liner. Instead of that I do this:


``` shell
#! /bin/bash

for file in $(find . -name "*.png")
do
  echo $file
  mv $file $file
done
```

I learnt that I can execute commands using `$(my_command)`.

Spl thanks to AliceGdj for asking me this question.
