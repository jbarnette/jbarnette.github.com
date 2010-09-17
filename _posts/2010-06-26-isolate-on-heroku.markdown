---
layout: post
title: Isolate on Heroku
---

**Update**: Jamie Macey wrote a [gem][] for this, and we improved the
logic a bit. Use it.

[gem]: http://github.com/jamie/isolate-heroku

Quite a few people have asked about using [Isolate][src] on
Heroku. There's no built-in support for Isolate in Heroku's current
deployment tools, but it's pretty easy to hack together using Heroku's
support for a `.gems` manifest file.

[src]: http://github.com/jbarnette/isolate

## Assumptions

1. You're using some sort of `rake release` task for deployment. See
   "Alternatives" at the end of this post for, uh, an alternative.

2. You're using Isolate with its `:system` option set to `true`. If
   you're using Isolate 2, this is the default. `:system => true`
   allows isolated projects to use gems that are already installed on
   the system, which is necessary for Heroku support.

3. I'm testing this with a simple isolated Rails 2.3.8 app, but the
   process is basically the same for any Rails version (or other
   framework). See the examples in Isolate's `README` for details.

## Dot Gems

Heroku's `.gems` manifest is a simple text file containing one gem
dependency per line, in a format that's very similar to a `gem`
command line. Heroku will read this file every time you release/push
reinstall all your gem dependencies if it's changed.

We're going to generate `.gems` from our Isolate file. Here's my
`lib/tasks/isolate.rake` file:

{% highlight ruby %}
desc "Generate a .gems manifest."
task :dotgems => %w(Isolate lib/tasks/isolate.rake) do
  File.open ".gems", "wb" do |f|
    entries = Isolate.sandbox.entries.sort_by { |e| e.name }

    f.puts "isolate --version '= #{Isolate::VERSION}'"

    entries.each do |entry|
      next unless entry.matches? "production"

      gems  = [entry.name]
      gems << "--version '#{entry.requirement}'"

      if entry.options[:source]
        gems << "--source #{entry.options[:source]}"
      end

      f.puts gems.join(" ")
    end
  end

  abort "Commit .gems, it changed." if /\.gems/ =~ `git status`
end
{% endhighlight %}

This task looks at all your isolated gem entries, picks the ones that
are valid for production, and writes each of them to the `.gems`
file. It also adds Isolate itself as a dependency. If `.gems` has
changed, the task aborts and reminds you to commit the changes.

## Releasing

My `rake release` task does a fair amount of stuff before it pushes to
Heroku, like creating a release email and running some sanity
checks. To make sure my gem dependencies are always up-to-date, I just
make sure the `release` task depends on `dotgems`:

{% highlight ruby %}
task :release => :dotgems
{% endhighlight %}

Done. Any time I run `rake release`, `.gems` will either be up-to-date
or prompt me to commit the changes before continuing.

## Alternatives

This works Well Enough for me at the moment, but it could certainly be
smoother. If you deploy using `git push` instead of wrapping it in a
Rake tasks, you could use a Git pre-commit hook to regenerate `.gems`
if necessary.

Isolate 2 has added some [lifecycle event hooks][hooks], so it'd also
be pretty easy to autogenerate `.gems` every time Isolate runs.

[hooks]: http://github.com/jbarnette/isolate/blob/master/lib/isolate/events.rb

Of course, the best possible solution would be for Heroku to support
Isolate natively, but I wouldn't hold your breath for that. :-)
