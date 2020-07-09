I tend to mentally divide code into roughly two types: "computational" and "plumbing".
Computational code handles your business logic. This is usually in the minority in a typical codebase. 
What it does is quite well defined and usually benefits a lot from unit tests ("is this doing what we intended"). 
Happily, it changes less often than plumbing code, so unit tests tend to stay valuable and need little modification.

Plumbing code is everything else, and mainly involves moving information from place to place. T
his includes database access, moving data between components, conveying information from the end user, and so on. 
Unit tests here are next to useless because 

a) you'd have to mock everything out

b) this type of code seems to change frequently and 

c) it has a less clearly defined behaviour.

What you really want to test with plumbing code is "does it work", which is handled by integration and system tests.
