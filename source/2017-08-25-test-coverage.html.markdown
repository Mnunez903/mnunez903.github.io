---
title: Test Coverage - going from bad to good, and knowing when to do it
date: 2017-08-25 17:24 UTC
tags: Test-Coverage
---
# Test Coverage - going from bad to good, and knowing when to do it

Having production code with good test coverage is very beneficial to a development team.
Broad coverage can catch bugs and unintended behavior from entering the codebase, and everyone can sleep better at night, but when a code base doesn't have much coverage (or any at all), it can be really difficult to introduce it.
We'll discuss when you should introduce or increase test coverage, and go in depth into the ways in which it's beneficial for you and your team.

## Coverage for legacy codebases?

As a huge believer in tests, I make a concerted effort to add coverage to every project I work on.
Realistically though, there are times where tests are just not that beneficial.
For instance, when dealing with a legacy codebase (an internal API that is rarely updated), adding coverage offers diminished returns.
If your legacy codebase works reliably in production with little to no regression, adding tests retroactively may simply work to verify what is already validated in production.
Often, the legacy parts of an application serve as dependencies, so I suggest focusing your efforts toward testing the new API leveraging the old code.

## Still unsure of the benefits to coverage?

Here are some benefits to increased test coverage:

- Ensure your code works as expected
- Deploy code with greater confidence
- Decrease the likelihood of 1am phone calls
#### **Ensure your code works as expected**
Adding tests encourages you to conceptualize how you want your program to behave and account for edge cases.

#### **Deploy code with greater confidence**
The greater your coverage, the more confident you can be that new features did not introduce regressions.
In the event that deployment introduces a bug, tests can serve as documentation to both track down the bug and squash it.

#### **Decrease the likelihood of 1am phone calls**
Pager duty is not fun. Seriously.
Nor is it fun for the person calling you.
Increased coverage will help prevent bugs that have the habit of waking you up in the middle of the night.
Future you would appreciate that.

## Okay, I'm sold! How do I start adding coverage?

Once your team is on board with increasing test coverage, I suggest first writing test for new feature work.
That way, new changes to the codebase are covered, and good habits will start to form amongst team members (and in turn, new hires).

Your next priority should be adding coverage for existing code (non-legacy), but this must be done much more carefully.
There are generally two ways to go about it:
- Scrap the existing implementation, one discrete module at a time, and test drive the recreation of its code
- Add tests to validate the existing code.

#### **Scrap & test drive**
Pros:
- Scrapping and test driving will likely result in better design and code clarity.
- The tests will serve as a form of documentation for your teammates and future self.

Cons:
- Throwing out existing code can result in you missing a particular business case that wasn't clear within the implementation.

#### **Add coverage to pre-existing code**
Pros:
- Generally a quicker process than scrapping and test driving
- Coverage of an existing API can make refactoring easier

Cons:
- May work to simply validate poor design.

## Side effects
Testing certainly has a learning curve, so your team may spend up-front time figuring out how to best test new and old code.
This can result in a decrease in sprint velocity, and may require more complexity points in story estimation.
That said, adding tests to new features will reduce bugs, and in turn, decrease the cost of having to squash them later,
and adding coverage to existing code will pay down technical debt that can prove crippling if left unpaid.

## Summary
To wrap up, increasing test coverage will improve design, increase team confidence and cohesion, and decrease the stress associated with regression.

Happy writing test coverage!!

![Writing code like a GOD](https://img.devrant.io/devrant/rant/r_536209_rcy6p.gif)
