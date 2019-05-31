---
layout:      post
description: >-
  My views on writing testable code.
image:       assets/images/beaker-biology-chemical-1366942.jpg
categories:
  - software-development
comments:    true
---

*Recently I did a poor job explaining some of my code decisions to another
developer, so here's my attempt to do a better job of that...*

Code design & architecture are important. Testability is important.
But over the years I've taken issue with the code produced by some of the prevailing design philosophies in the software development industry.

## Tests *are Greater than* Testability

Over the years, I've seen people make a lot of architectural decisions in the
name of testability, but then neglect to actually write any tests... or just
write meaningless "fluff" tests: "should be able to construct object" or similar tests.

**Actually writing tests is more important than creating a testable architecture.**

You would think that testable code would be a pre-requisite for writing tests, and it is, but **it is the process of writing the tests that properly shows you what is needed to make your code testable**.
Otherwise you may wind up creating lots of needless abstractions and layers that don't serve any real purpose, and purposeless code is dead weight that slows down the development of an application.

## Hammers and Nails

"When you're a hammer, every problem looks like a nail." People like to apply the same solution they are familiar with to every problem.  When it comes to writing testable applications, there are *lots* of options, some better for certain scenarios than others, but many developers use the same trick over and over: constructor dependency injection. Read [Working Effectively with Legacy Code](https://www.amazon.com/Working-Effectively-Legacy-Michael-Feathers/dp/0131177052) by Michael Feathers for an awesome explanation of the many different techniques available to developers.

## Complexity vs Consistency

Try to build your code as simply and cleanly as the problem allows.

Each requirement your application must meet necessitates a certain level of complexity in the resulting solution.
Automated testing is a requirement that most (maybe all) applications should have, a requirement that does add some measure of complexity to the solution.
It might be a small amount of complexity, but it's still *some*.
For example, your application is going to need a few more moving parts than it would without tests - you might need to be able to swap in fake data access code, etc.

The desire for *consistency* sometimes drives us to create solutions that are more complex than strictly required. We might opt for a more complex solution in one area of our application in order to maintain a similar architecture with a different area of our application. This isn't necessarily bad - but the decision to do so should be weighed: does the benefit of this consistency outweigh the added complexity?  Sometimes the answer is "yes", because sometimes making one area more complex can make the overall solution *less* complex - because there are fewer specialized approaches within the one codebase. Sometimes the answer is *no* - and it may be OK to break consistency in order to not raise the complexity of the app.

## So... What?

Maybe I'm still doing a poor job of explaining myself. I prefer to slice my applications vertically (by feature) rather than horizontally (by layer). I prefer to introduce abstractions, layers, etc. as needed, rather than preemptively. I don't feel bound to one method of breaking dependencies for tests. And tests are more important than testability. I believe this approach ultimately results in easier to test and easier to maintain code.
