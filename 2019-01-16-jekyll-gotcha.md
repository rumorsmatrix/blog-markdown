---
title: Jekyll gotchas
tags:
 - blogging
 - programming
 - ruby
 - jekyll
---

A few days ago I decided it would be a good idea to try writing my own blogging CMS (again). I wanted to experiment with `composer` and `altorouter` and yet another blog seemed like a good testing ground. 

After making [a bit of progress]() and learning about markdown and YAML parsing, I ended up installing a couple of different static site generators, and was pleased to see that they seemed to handle templating pretty much how I had implemented it myself, [dependency injection](https://phptherightway.com/#dependency_injection) and all. Satisfied I was doing it right, and now totally enthralled with the idea of keeping a blog as plain text in a git repository, I turned to [Jekyll](https://github.com/jekyll/jekyll). After all, the three virtues of a programmer are [*laziness, impatience and hubris*](http://wiki.c2.com/?LazinessImpatienceHubris), and what's the point of re-re-re-inventing the wheel?

So I set up Jekyll, made some tweaks to the default template, learned a little about Ruby's `gem` ecosystem. Added tagging and pagination. Started backporting posts from my old WordPress and Tumblr blogs. Eventually I want to collate my "best of" from my various scattered websites and place them all here -- and into source control, so they'll be safe.

So far I've noticed two "gotcha" issues while using Jekyll, which I will place here for future reference:

- If you `gem install` a gem and don't add it to your `Gemfile`, when you run `jekyll build`, one of two things will happen. If your working directory is your jekyll project, everything is fine. If not, the build will proceed but warn of the missing gem and not have access to it. 

- If you use the `-d` flag on `jekyll build` to specify an output directory, the build process will remove any symbolic links in the destination directory. This was a head scratcher for a while, but [it's a documented issue](https://github.com/jekyll/jekyll/issues/3095). 

Apart from that, it's been smooth sailing, and I'm really happy with Jekyll and the prospect of gathering all my stuff together in one place. To help speed things up a little, I've added this line to my `.bash_aliases` file:

```
alias jb='JEKYLL_ENV=production jekyll build -s ~/jekyll/ -d ~/jekyll/_site/ && cp -R ~/jekyll/_site/* /var/www/html/rumorsmatrix.com/public_html/'
```

Happy blogging!

