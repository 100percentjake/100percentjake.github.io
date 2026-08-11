---
title: "Making a 10KB CMS with AI"
date: 2025-11-11
---

![[img/chatgpt.jpg|ChatGPT logo]]

Sometimes the thing you want doesn't exist. Or it does but only meets 99% of your requirements, and the last 1% is so annoying you end up delving into the deepest depths of 10 year old Reddit posts. For everything else there's MasterCard.

## But y tho

Listen, I have my fair share of experience with Wordpress. I've done my time in the depths of Dependency Hell trying to manipulate the bloated, terminal-feature-creep mess of a "framework" into looking good while also performing well, stacking technical debt onto even more technical debt. Not that standalone CSS frameworks are much better, drowning me in more features than I could ever hope to require. I just wanted a simple, quick loading CMS with no database, no PHP requirement, and no backend whatsoever. My backend is SSH file transfer, go fuck yourself.

## AI?

Let me be clear (Obama.avi). I hate the current state of "AI", "AI" in quotes because GPT isn't AI, Stable Diffusion isn't AI, and a neural net is not "artificial intelligence" though it could be argued that it is the close. What we do have is a generation of extremely useful tools that all came out at roughly the same time and are all extremely good at very specific things. If you use ChatGPT to generate slop "novels" and spam Amazon with them, I hate you. If you use a neural net-based audio generation software to flood streaming services with fake "music", I hate you. If you generate "artwork" that was trained on the work of genuine artists and flood fansite, etsy, amazon, etc. with it all, I hate you. Please jump into the nearest convenient wood chipper.

However, all of these tools have legitimate extremely useful use cases.

Neural audio algorithms are next-level for noise reduction, audio level processing, voice isolation, and other extremely useful tricks. Image generation and processing is incredible for background separation and some touch-up work. And GPT is useful for a myriad of things. I am most excited for the expansion of so called "RAGs" that feed your documentation base and files into an (ideally locally-hosted) LLM instance and it is then able to answer questions based on them. Can't remember what file has that thing with that stuff? A RAG could tell you what file that's in, and since it's instantly verifiable you aren't limited by the chance that the RAG is hallucinating. I also appreciate LLMs for quick and dirty inspiration. "Make me an outline for" blah blah blah. Lovely.

But lately there has been a new use case coming out that has spawned an entire culture of 'vibe coders', where LLMs are being used to quickly generate functional code, be it HTML, JavaScript, Python, C++, etc. 

Now obviously the morals here are murky for similar reasons as the AI generation; an LLM is trained on something, and in almost every case that "something" is the public Internet and whatever purchased content the owning company was able to get their hands on to give their model a competitive advantage.

This is a quandary I will be ignoring for the time being.

## Let's make a website

There are a number of LLMs out there that are optimized for code creation and revision, and I chose initially to ignore that in favor of ChatGPT for no reason other than I wouldn't have to log into it.

So what do I want to make?

* One page blog site

* No server-side processing

* Responsive

* Support images

* Slug links for individual posts

* Paginated

With this in mind I fed a simple prompt into ChatGPT

`Make a basic paginated single column blog website that dynamically loads posts from .txt files with multiple inline pictures, and provide a demonstratory .txt file. Make the design minimal and modern.`

My "development environment", if you could call it that, was pretty unsophisticated. A basic web server running on my Synology would be the test site, and I would be pasting code from ChatGPT into VSCode which would have the Synology's files open. To my mild surprise the first batch of HTML from ChatGPT did in fact open and render. It also provided me with a diagram of the file structure.

```text
/blog/
│
├── index.html
└── /posts/
    ├── posts.json
    ├── post1.txt
    ├── post2.txt
    └── post3.txt
```

In this system some JavaScript in the index.html would read posts/posts.json which would have a list of all of the posts.txt files for it to then enumerate. Neat. Interestingly after listing all of the code and explaining it briefly ChatGPT offered to add a dark mode toggle.

Might as well.

A few seconds later ChatGPT had generated an entire new index.html file, which worked, and suggested some new features.

`Would you like me to add smooth transitions (fade/slide) when switching between posts or toggling dark mode? It would make the reading experience feel even more polished.`

Hell, why not? But also I had it address some alignment issues with the previous/next page buttons, and wanted it to add slugs to the URLs.

After mansplaining to me what slugs were (really?) using entirely too many emojis my new features were present, and the alignment issues persisted. What followed was a a cycle of adding features while requesting a bug fix, getting my feature, and the bug getting half fixed, if that. 

- Dark mode? Done.
- Slugs? Done.
- Inline images? Done.
- Highlighting the active page in the sidebar? Done, but now the sidebar alignment is thoroughly fucked.

It was at this point that ChatGPT also stopped rendering the entire HTML every time a change was requested, instead just offering me code snippets and expecting me to insert them into the existing code manually. The fuck? I'm not here to do *work*, that's why I have hallucinating autocorrect writing this second-semester computer science course tier garbage for me. A swift reprimand to Sam Altman's curse on the world put a quick stop to that, luckily.

The problem at this point was that the sidebar left-right alignment and the up/down alignment could not be fixed simultaneously for reasons I didn't care enough to figure out. After enough revisions I got kicked off the "good" ChatGPT algorithm I relented and had it create me a floating sidebar, and asking it to add alt-text functionality to images for accessibility reasons broke images completely.

At this point I was seconds away from switching agents to something more code-oriented like Claude. One nice thing about GPTs (at the time of writing, at least) is that they are non-deterministic. They have no memory, they don't remember their past actions. Every time you hit enter the entirety of your conversation thus far is fed back through the LLM. This means that were I to move to Claude it would, in theory, have no less understanding of my duct taped HTML than it would if it had made it itself. In a pinch, I think it's possible to feed it the entirety of my conversation with GPT and its understanding would be identical.

However, it didn't quite come to that, and after a couple more revisions the alignment issues were fixed and we were, to my knowledge, feature-complete.

## Putting it together

At this point I had a very blank starting point and needed to actually customize and populate it, which was very easy with VSCode. Changing colors, adding logos, tweaking a few things here and there and fixing a few rendering issues like the "Back to all posts" button not having proper styles attached to it. Things that would have been like pulling teeth to get GPT to execute on correctly. 

A quick hour or so of work and we have what you see here. A full dynamic CMS within 10kb that will run on noting more than a basic web server.

For the hell of it, here is the entirety of what ChatGPT spat out to me. Feel free to use and customize it, lord knows I don't feel arrogant enough to insist on some sort of license for code that was spat out of a supercharged autocorrect algorithm.

I'd love if someone who is experienced with web development could look this over and tell me how awful it is. I'm genuinely curious. 

[Here is a zip of what I've dubbed "Femto CMS"](../files/femtocms.zip)

Thank you for reading! 
