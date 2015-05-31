---
layout: post

title: "Large Scale iOS Development: Case Study"
cover_image: scale-preface.jpg

excerpt: "Part one, of a series of posts about developing and maintaining a large scaling project. This entry talks in high level, the problem and solution"

author:
  name: John Hatvani
  twitter: jhatvani
---

This starts part one of a many part series on scaling iOS development. By scaling
I don't mean adding more CPU or more nodes. I mean evolving an existing codebase with
a big and evolving development team.

The following is a recollection (some retrospective decisions) of a project I was
involved with a while ago and what we did.

## Case Study

Inheriting a codebase is not the best of situations especially when the original
developers/lead had made no attempt to build a scalable solution nor did they have
the foresight of what this codebase would turn into. Code where logic is not separated
into its distinct layers, repeated code, Observers that trigger other observers,
business logic in the view layer, just bad everywhere you turned.

If we were going to maintain and scale this codebase, we had to drastically rethink
the organisation of this project and a complete refactor was out of the question.

Luckily the code we were contracted to do was a complete new feature set so we did
not need to really touch the existing code base all that much.

## Implementing changes.

* Testing --  This was our biggest concern at the beginning, retro-fitting both acceptance
and unit tests on the existing code base. That make it easier to refactor/abstract large
segments of the existing codebase with (less) worry about regression.

* Continuous Integration -- At this stage with out projects separated and regression suites complete
we had the project building, testing and deploying on every commit.

* Project Abstraction -- By the end we had split the application up into several distinct
projects, Built into static libraries and resource bundles.

* New Features -- At this point we began implementing new features. With new features came new complexity,
new projects and dependencies.


And thats basically it, not only did we successfully (on time, budget) deliver the software but were able to fix
many performance bugs and memory leaks which existed in the code.

Future posts will address the key points in detail with (some) implementation detail
and tutorial.
