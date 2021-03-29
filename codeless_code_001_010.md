[001](http://thecodelesscode.com/case/1)

What is small/minor? This looks like a an observation on minor and impactful-ness on the piece of the system.

The toe is broken, and yet the body is functional, with all its pain.

[Case 2](http://thecodelesscode.com/case/2)

A bit morbid in my opiniion, this talks about how requirements are implemented.

There will be inherant disconnect between the business and the programmers because of the biases and 
assumptions brought to the table by the programmers(and the business).

I can understand what I read; I can understand what I can hear; I can understand what I can observe.
But there are always going to be edge cases that can be attributed to the "Unknown Unknowns", the title of the chapter.
That is something that can not be escaped.

[003- Encapsulation](http://thecodelesscode.com/case/3) 

I find this "story" to be a bit amusing. 
What I think the master is trying to inform the young monk is that data has to flow through the correct abstractions before entering the system else,
it is going to cause unintended outcomes.

Encapsulation allows us to ensure that this is enforced.

[004 - Willows](http://thecodelesscode.com/case/4)

I did take some time to realize this. I felt that there was insufficient information for judging what is correct. The below is my interpration of the koan

This is a refleection on the ability to recognize potential and understanding feedback, and using judgement when applying it.

The new priest was let go because they were unable to recognize and judge what is grass, what is willow, what is mutable and what is not,
and the potential of their subordinates.

And thus, `We cannot lie across a thousand willows and contemplate the sunrise.`

[005 - Void](http://thecodelesscode.com/case/5)

What is Void? 
It is nothging. It is everything and anything the programmer wishes.

In imperative C style programming language:

It is the value returned by a method that does not return anything. It can be used to point at any datatype.
It is used to indicate the absence of a value.

In function programming, it is used to indicate side-effects from a function.

Being in a mostly OOP-imperative style environment, I'm unable to contemplate the mening of `void` in functional programming. Hopefully, I will be able to add more here once I grain more experience.

[006 - Empty](http://thecodelesscode.com/case/6)


This koan speaks about null and null returns.
Returning null in general is a bad practice. Instead of returning a null, return a null object(in this case, an empty array).
This way, the calling method doesn't need to do a null check.
Also, raising exceptions just because there is no data to be returned is incredibly annoying. Normal program flow should not throw exceptions

[007 - The Enemy of the Good](http://thecodelesscode.com/case/7)

Perfection is unattainable. 

We must work with what is good enough.
To be able to work with what is good enough, we need to ensure that it is actually good enough.
This confidence is given to us by doing manual testing and by writing automated tests.
Testing is not a distraction, but an essential part of software development process,
so as to ensure the correct working of what is being produced.

[008 - Reduce, Reuse, Recycle](http://thecodelesscode.com/case/8)

```
A novice asked the great master: "What is the Way?"

The master replied, "Writing code is the Way."

The novice then asked, "What is not the Way?"

The master replied, "Writing code is not the Way."

The novice said, "Then the writing of code is all things."

The master replied, "And the not-writing of code also."

The novice asked, "At the present moment, are we writing
code, or not writing code?"

The master replied, "We are the code."
````

When I am code and yet not code, when the project is code and the people and the people are code, there is nothing more to say.

[009 - Infinite](http://thecodelesscode.com/case/9)


The question here that is posed to the reader is that, what is the nature of the infinite?
Does the program end when the user exits it or when the machine stops ?

[010 - Pride](http://thecodelesscode.com/case/10)

How much proud should a programmer be?
Pride is one of the 3 qualities mentioned by Larry Wall(Laziness, impatience and hubris).
The pride of the programmer should not blind them from seeking/reusing solutions that are already available.
Pride should not be the cause of becoming anti-social, since software development is an extremely social activity,
where communication with fellow programmers and stakeholders should be taking the highest priority.
So much of a high priority, that code itself should become a vehicle for communicating ideas across the team.
