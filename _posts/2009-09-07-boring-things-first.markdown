---
layout: post
title: Boring Things First
---

*[This is a draft.]*

Yeah, yeah. You're agile. You *always* test first, you work in tight
iterations, you have YAGNI tattooed on your forehead. Good for
you. Guess what? You're building on sand. Do this stuff first:

## Tests (and Autotest) With Coverage

Make sure your testing infrastructure works. Write a single sanity
test, make it pass and fail, and make sure that your test
scripts/tasks, autotest setup, and coverage tools are working
correctly.

## Deploy/Install/Update an Empty App

Before you write a damn thing, make sure you can distribute. If you're
working on a Rails app, get your [Vlad][] or [Capistrano][] setup
tuned and perfect. Do a bunch of blank deploys.

[vlad]: http://rubyhitsquad.com/Vlad_the_Deployer.html
[capistrano]: http://www.capify.org/index.php/Capistrano

If you're writing a desktop app, write your installer and make sure
it's working. Don't wait 'til the last minute! The moment you write a
line of code, it'll be easier to have someone test it if the
installer's functional.

Even better, start by integrating an update system like
[Sparkle][]. You may be distributing the empty shell of an app, but
now you can automatically update your testers every time you push new
changes. And you're testing your post-release update infrastructure at
the same time! Win!

[sparkle]: http://sparkle.andymatuschak.org

## Error Notification

Some of your code is shit. Even in the unlikely event that all your
Codes Are Perfect, someone's code that you *depend* on is
shit. Integrate error reporting at the very beginning, before any
users have a chance to make errors. For Rails apps, I use
[Hoptoad]. There are a billion other alternatives, and rolling your
own is easy too.

[hoptoad]: http://www.hoptoadapp.com

## Fundamental Docs

You're probably not going to be the only person who works on this
project. How does the next person in the door get up and running? If
the answer is much more complicated than "check out the code and read
the README," you suck.

Start documenting at the very beginning. What should someone run to
get started in a fresh checkout? (I like `rake newb`) How does
deployment work? Where's the deployment server? How was it configured?
How do I stand up another one from scratch? What external services
(issue tracking, error reporting) does this app use?

Make sure your *initial* set of docs answers these questions, and make
it clear that keeping them up-to-date is as important as keeping the
tests passing.
