Sometimes databases don't support non UTF-8 chars.
Then I do the below to the strings that need to be saved:

``` ruby
"\xED\xB9\xBA\xED\xBE\xA5n V\xED\xB9\x9F\xED\xB4\xACe".chars.select(&:valid_encoding?).join

```
