---
layout: post
title: "Vim Induced Ego Depletion"
date: 2015-02-03 15:49:27
tags: vim text editor janus
---
There is a religious war being fought over what developers consider to be the
best text editor. I won't try to recruit you into the Vim army here, but I will
address one of its main criticisms: it doesn't do enough out of the box.

Of course, there is a [huge community][vim-scripts] around Vim plugins that
provide any and all functionality you could ever want from your text editor,
however there is an inherent cost in adopting and managing your own
configuration.

There is a pattern of developers maintaining their own dotfiles in Github to
manage this, and often you'll find their .vimrc is the file they're messing
with the most. Tools like [vundle][vundle] and [pathogen][pathogen] help
significantly, but they can't solve all the problems.

When I jumped on the Vim bandwagon I was enamored by all the choices available
to me. I imagined a world where my editor and I were so optimized for each
other that we were finishing each other's sentences, covering for each other
when we slacked off, and transcending what either of us could achieve on our
own. It was beautiful.

I think I made it a week, then it all came unravelled: some plugins were
showing their incompabitility with others, I'd spend hours each week tweaking
things, and my "always be upgrading" nature would get the best of me. I was
feeling the effects of [ego depletion][ego_depletion].

I began to stray, thinking I should go with [Sublime Text][sublime] at the risk
of being labeled a lazy hipster.

Finally I reminded myself of my own philosophy: trust domain experts to do as
much of my work and make as many of my decisions as I can. More often than not
I'll be left with a result that's as good if not better than if I spent the
time to weigh all the options and do all the work. This leaves me enough time
to work on other problems I'm good at or that haven't been solved yet.

[Janus][janus] to the rescue. Lots of people with tons of experience have
vetted and continue to vet the best Vim plugins and bundled it for all of our
convenience. It's easy to keep up to date (just run `rake` in your `~/.vim`
folder every so often). And for that rare case where small tweaks are still
needed [you're still covered][janus-custom].

Ego repleted. Street cred salvaged.

[vim-scripts]: http://www.vim.org/scripts/script_search_results.php
[ego_depletion]: https://en.wikipedia.org/wiki/Ego_depletion
[sublime]: http://www.sublimetext.com
[janus]: https://github.com/carlhuda/janus
[janus-custom]: https://github.com/carlhuda/janus#customization
