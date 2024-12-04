---
title: December Adventure 2024
css: assets/css/main.css
---

[←home](..)  
[↓Jump to present](#current)

## Preamble and Planning

I'm excited for [December Adventure](https://eli.li/december-adventure) 2024, where I'll code a bit every day of the month and write about it. Last year [I participated](https://leetusman.com/december-adventure-2023) and worked for a month on designing a new website. When the month ended I hadn't finished, and I ultimately made some different design decisions than I experimented with. But I did use a lot of the knowledge I gained, and I learned what I didn't want to do as well. In particular, I made comprehensive class-free CSS stylesheets, learned about automation with custom templates for pandoc, and developed approaches to building galleries with flexbox. I worked on image conversion scripts, and accessibility. I also learned about the limitations of using markdown and bash with variables as a templating language. All of this and much more I put to work in the class websites I made in the spring afterwards, and finally in my [website redesign](https://leetusman.com) that I completed in the spring.

This year, I don't have a single project but instead a number of little things I'm interested in exploring. I probably can't get to all of them. And I'll let myself wander depending on my interests. 

Currently, these are my ideas of things to play with:

* Work on an experimental narrative with recorded audio and 3d assets. Maybe in p5/WebGL, or maybe Lua
* Make a simple 3d environment in Godot, ideally with my own hand drawn assets
* Try out Construct 3 for rapid game-making
* Try out Jeffrey's [aesthetic.computer](https://aesthetic.computer).
* Complete my claw machine roguelike in Pico-8?
* Work on my Forth-based Processing-like little language, using SDL/Love2d on the backend
* revive the PocketChip, and try to see what I can do with it with its ancient OS
* Install alternative firmware for my Anbernic, and try adding the Pico-8 player to it and more roms
* Make some class sites with Hugo, possibly with Pandoc
* Play around with LOGO again, to prep for teaching with it in Drawing, Moving and Seeing with Code this spring

I probably will only try a small handful of these, but it's nice to have some options in mind.

Okay, I'll be back December 1. Let's see if I stick with this color palette!

## Nov 29

I started early.

I checked out [markdown-lichen](https://lichen.commoninternet.net/), a project by online/irl friends of mine. It's a gui wrapper around markdown-based static CMS. I did some testing in straight php and it worked mostly fine without being able to render built html pages. I had a chat with Max on Masto about implementing it to work without requiring docker, apache or nginx, since the goal is to be lightweight. They thought that should be doable. Will come back to this project and do more tests probably at that point. I guess I could always look into php myself but it does not fill me with joy. I'm hoping Max implements it, then I could add in documentation and run some tests.

Next I researched the [Picotron fantasy workstation](https://www.lexaloffle.com/picotron.php) to see if I wanted to purchase and play around with it. I found some cool projects, checked out the terminal, API, ran some programs online. Ultimately, I didn't find something to excite me enough to work on, so I'm going to pause on that for now.

Next, I worked on a web project. Some colleagues are in an exhibit opening in a month in LA and need a timebased 24-hour work to display in a website, updating once a second, as part of a show. Consider it something like a 24-hour long video with a framerate of 1 frame per second. They asked if I could make it happen. I developed a simple system and implemented a test, building out a simple site for them to check speed, image resolution, and for us to do some testing for robustness. Took me an hour or so for the initial test from idea to coding to deployment. Sent it along for their feedback. I should ask them for some money. I'll track my time. :)

By the way, this mini blog is being implemented in pandoc with front matter holding the title and css filename, and then just using a simple incantation in the terminal to render md to html.

## Dec 1

Okay, first official day of December Adventure. It's Sunday, and I spent much of the day staying warm, visiting Swiss Institute to see their current shows, and the tea shop and Ukrainian Village.

In the evening I decided to spend some time evaluating static site generators and to build one up because I've been unhappy with jekyll. For a decade I've mostly used jekyll, which has built-in support for GitHub pages. This means it's easy to host websites on GitHub written in Jekyll. But every few months when I try to make a post on one of my sites (class sites or project sites) I run into a problem and the site won't build due to dependency hell from some combo of Ruby, gems, or bundler dependencies. I don't want to use any of these. I've put checking out hugo on the back burner for a while, so now felt like a good time to spend a little time with it. 

I tried it in 2017, wasn't immediately noticing it to be much superior to jekyll, and haven't tried it out since but every time I complain about jekyll someone recommends hugo. So I checked it out! Unfortunately, to make a new site I have to invest time to figuring out directory structure, configuring templating and themes. And like Jekyll, it has many variables, and such to learn and implement. I know it's probably faster than building my own site from scratch but I got turned off. I didn't want to learn the hugo way. 

So next I fired Eleventy/11ty static site builder, and I check out the starter example on glitch.com. Based on this starter, the structure is pretty clear. The default nunjucks templating can be switched out for liquid templating, which might make it easier to switch. I do have to say I'm not thrilled about npm/node.js here as I fear there could be the typcial npm ecosystem of pulling in a million dependencies, and again dependency / version hell, though npx is to try to prevent this I guess. But based on being a retrogrouch I next pulled up bashblog, a ssg written in pure Bash. It's fine, though it spends a lot of lines adding in google analytics, disqus and twitter stuff, among other things I do not need or want. I also find the code hard to read since it's bash. And the default theme is ugly, and the project creator abandoned it, so maybe it wasn't great? 

To make a long story longer after all that I returned to my own custom bash and pandoc-based static site generator, panblog, which I started years ago. I had extracted minimal parts for powering this mini december-adventure site for example, so this was the kick in the pants to complete it, completing a build script, adding in theming, permalinks, index page builder, and auto-adding headers/footers, and rss feed generation. These are all things I already can do, so just need to automate it intelligently. 

So I picked up where I had left off working last time I touched the repo. Thankfully, I'm pretty good with documentation and left lots of notes. I decided to make some assumptions, but allow things to be easily changed. There is a config.conf file that holds the sub-directories for: themes, which are just css files; posts, which are markdown files with YYYY-MM-DD-name.md naming scheme; assets, the image assets source directory; templates, a folder holding html templates for pandoc to convert md to html for different kinds of pages; and some variables for holding the site name and url, for example. 

My build script creates a site folder if needed. It loops through the posts folder of markdown files, extracting the name and the date separately, via hacky regexes that took me a while to get right. My build script adds the post name and a link to the post page, inside its own directory, to the index page. It then adds the extracted date. It does this in reverse order so the most recent blog posts are at the top of the index. It uses pandoc to convert each post and the index page from markdown to html. I also set up a separate assets folder to hold images. Next steps are to add back in page conversion for non-blog pages, and then to test and automate the rss feed generator. Then to make sure I have some couple good basic and different classless themes. If all goes well, I think this could become my new static site generator for my uni classes, and maybe for my sites in general, and then maybe a good tool for other folks to use as well. It threads the needle between basic markdown to html conversion with straight pandoc on the one end and an overly complex ssg like hugo on the other. I think it's well on the way.

![panblog test](assets/img/panblog-test.jpg)

## Dec 2

Added a lot to my [panblog](https://tildegit.org/exquisitecorp/panblog) static site generator including a comprehensive build script, configs error checking, page rendering system, and documentation. I did a variety of tests and found a few bugs I still have to crack but am in overall good shape. 

<div id="current"></div>

## Dec 3

Much of the day has been consumed by me sitting on a couch with a laptop open and trying to crank out a professional document I have agreed to write, outside of my job but in keeping with the expectations of academia, to support faculty at another institution. It is not due until next Monday but the institution keeps asking me for it, so I'm trying to knock it out. Unfortunately it's been to the detriment to finishing up squashing bug on panblog. 

Anyway...I did get some time to work on it. So far I removed some old build scripts, tested my non-post page generation a bit, then added in some build automation to include opengraph (og:meta) tags, though ran into some issues when trying to populate the opengraph tags. 

Next I spent some time researching both metadata and front matter [variables](https://pandoc.org/chunkedhtml-demo/6.2-variables.html) in pandoc, with the goal to automate pulling a og:image url from frontmatter . I think I found a solution through the `--metadata KEY[=VAL]` option or the front matter, and finally found a [good explanation on stackoverflow](https://stackoverflow.com/a/26490978), that I think will be useful and I plan to use that to try to knock out remaining needs for populating variables. I also see useful info in the extensive man page `man pandoc` in the TEMPLATES section and then in Conditionals, which I think will be useful for testing if an image is set and then assigning the og:image metadata if it is.

Lastly for panblog, I began to rework gmi.css to an alternate "good defaults" new theme to ship with panblog. First, I checked out [2-color palletes](https://lospec.com/palette-list) from the Lospec website, and began trying some options, building out a new starter theme fresh.css.

Also, separately, I squashed a bug on [Archiving Artist-Run Spaces](https://leetusman.com/archiving-artist-spaces/) and added a redirect to my main/portfolio website in the /projects sub-directory in case anyone tries to manually go there directly (instead of to a project directly) so they are re-routed to root, which is the actual portfolio landing page, instead of a 404.

[↑top](#)
