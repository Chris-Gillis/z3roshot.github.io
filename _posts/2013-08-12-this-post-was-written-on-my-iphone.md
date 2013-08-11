---
layout: post
title: How I blog from my iPhone
---

[MacSparky](http://macsparky.com) [wrote an article](http://macsparky.com/blog/2013/5/put-your-mac-to-sleep-with-ios-drafts) about a method he conceived to lock his MacBook from his phone. I thought it was so clever when I first heard it. I don't have a MacBook, but oh boy, the first thing I do when I get one is set that up. 

I didn't know it at the time, but that process would morph in my head to the process I am using to write this blog from my phone. I'm particularly geeked out about this process, so I wanted to share how I'm doing this.

## the tools
 {: .orange}

###[Drafts](http://agiletortoise.com/drafts/)

[Merlin Mann](merlinmann.com) has talked about drafts a number of times, and for
good reason. Simply put, you open it up and start writing text. When you're done
with that, you can perform an action on the text. It also has integration with
[DropBox](http://dropbox.com), [Twitter](http://twitter.com), [Facebook](http://facebook.com),
[Evernote](http://evernote.com), and even the standard email and messaging on your
device. The relevant one for this discussion is DropBox, but we'll get to that
later.

###[DropBox](http://dropbox.com)

Dropbox doesn't need an introduction from me. Their tag line is "Your stuff,
everywhere". This is essential to my setup.

###[Hazel](http://noodlesoft.com/hazel.php)

Hazel is one of those tools that I didn't get at first. I thought it was neat,
but I didn't have any uses for it that could justify paying for it. Since
thinking that, I have seen the light, and I would be much less happy in my
computing life without it. Hazel will watch directories for changes that you
specify, and then carry out actions that you tell it to. One thing I use it for
is to watch my wife's DropBox for pictures and automatically backs them up to my
computer. I never have to think about it, because it just happens. The only
limit on this tool is your imagination. Did I mention it can run shell scripts
or applescripts?

###[Jekyll](http://jekyllrb.com) and [GitHub Pages](http://pages.github.com/)

This page is hosted on GitHub pages. The engine that generates the pages is
jekyll. This part of the setup is pretty standard so I won't go into how this
works. It doesn't need to be said that I'm also using git for this, which is
implied by me using GitHub.

##the secret sauce
 {: .orange}

By this point you may have figured out my process, but I'm going to lay it out
anyway for my own benefit.

1. Open Drafts on iPhone
2. Write article
3. Use DropBox action to save file to a specified folder in DropBox (For me -
   DropBox/Apps/Drafts/BlogDrafts)
4. Hazel sees this new file and moves it to my local git repository for my blog.
5. Hazel renames the file to follow jekyll conventions.
6. Hazel runs the following shell script:

<script src="https://gist.github.com/z3roshot/6200811.js"></script>

And GitHub handles the rest.
A couple things to note: I don't actually want to automate the final step of
making my posts public, so I put them in a "drafts" directory in my repository
so I can proofread and edit and then I have a script that I run manually that
moves the file to the normal posts directory.

And now you have all the pieces you need to write posts from your phone!

_I do have a confession to make - I started writing this on my phone, but I
finished it on my computer because I needed to do a bit of research, and it's
easier on a computer. If you have a bluetooth keyboard, there's no reason you
can't blog directly from your iPad._
