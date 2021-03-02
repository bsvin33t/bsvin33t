[006 - Empty](http://thecodelesscode.com/case/6)


This koan speaks about null and null returns.
Returning null in general is a bad practice. Instead of returning a null, return a null object(in this case, an empty array).
This way, the calling method doesn't need to do a null check.
Also, raising exceptions just because there is no data to be returned is incredibly annoying. Normal program flow should not throw exceptions

