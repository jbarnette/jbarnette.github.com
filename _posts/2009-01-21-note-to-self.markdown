    ---
    layout: post
    title: Note to Self
    ---

## Be Confident

Tests build confidence. Write 'em. They'll save your ass, and they'll
let you take a chainsaw to your code without being afraid of unintended
consequences.

## Be Lazy

Write tools. If it's happened more than twice, don't ever do it by hand again.

## Be Asynchronous

If it can be done outside the request/response cycle, consider queuing it.
Mailers, uploads, audit trails, anything with an external system dependency
or a lot of IO.

## Be Stateful

If there's a lifecycle, model it as a real state machine. Beware ad hoc flags.

## Be Clear

You'll write it once, but you'll read it a lot. Code accordingly. Sometimes
simplicity takes a bit longer, but it'll pay off.

## Be Consistent

Inconsistent file names, task names, and coding styles hurt productivity.

## Be Timely (but not too timely)

Keep frameworks, plugins, libraries, and tools up-to-date, but think twice
before using a production app to play with the bleeding edge.

## Be Certain

Don't speculate, get data. Act on what you know, not what you suspect.
Is that code really faster? Do users really want that feature?

## Be Persistent

Find the root cause. Keep asking **why**, even when you're tired and under
the gun. The guesswork patch you write today will be a nightmare tomorrow.

## Be Wrong
If it's not working, change it, no matter how long
it took to write. Don't throw good money after bad. Admit mistakes early
and often.
