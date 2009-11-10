---
layout: post
title: Deploying to Heroku
---

Deploying to Heroku with `git push` is awesome. I'm running a couple
of different environments, though, and there's extra stuff that I want
to do when I deploy. Rake to the rescue!

## Some Assumptions

Okay, here's how I roll: `origin` is GitHub. `origin/master` is the
production branch, *not* the head of development. `origin/next` is,
well, what's next (you probably call it "staging"). There are local
tracking branches for each of these, natch.

New features happen in topic branches, and they're merged into `next`
when they're ready. Emergencies and bug fixes are similar, but they
also get merged into `master` and deployed before `next` is fully
baked.

`master` is only ever updated by bug/emergency branch merges and
periodic merges of `next`. If `git merge next` isn't a fast-forward,
something's probably wrong.

There are (at the moment) two Heroku environments, `myapp-next` and
`myapp-production`. There's a Git remote for each environment:

    $ git remote
    next
    origin
    production

Got it? Good.

## Deploying

    $ rake deploy

*Super* complicated. In my setup, this task...

* regenerates a Heroku `.gems` file and complains if it's out-of-date,
* complains if I'm trying to deploy from a branch that doesn't match
  an deployment env (deploys can only happen from `master` and `next`),
* sets the `TO` environment variable for Hoptoad,
* shows a list of all the changes since the last deploy, and how long
  it's been,
* pushes the current branch to the matching remote, e.g., `git push
  next next/master`,
* tells Hoptoad about the deploy, and
* sends a fancy email w/changes to the deployment mailing list.

## The First Time

    $ rake deploy:newb

This task installs the `heroku` and `taps` gems if they're not
available, creates and fetches the Heroku remotes for each
environment, and makes sure you have local tracking branches for the
`origin/bleh` equivalents of each remote.

## What changed?

    $ rake deploy:pending

This task shows a list of commits that have happened since the last
deploy. It's a pretty thin wrapper around `git log`.

## I Hate Conclusions

There are a few other lifecycle hooks for attaching stuff that needs
to happen before or after the deploy, but that's pretty much it. A
lightly edited version of my `lib/tasks/deploy.rake` is available in
[this Gist][gist]. Add to it, correct it, abuse it.

[gist]: http://gist.github.com/231216
