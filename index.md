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

<div id="current"></div>

## Nov 29

I started early.

I checked out [markdown-lichen](https://lichen.commoninternet.net/), a project by online/irl friends of mine. It's a gui wrapper around markdown-based static CMS. I did some testing in straight php and it worked mostly fine without being able to render built html pages. I had a chat with Max on Masto about implementing it to work without requiring docker, apache or nginx, since the goal is to be lightweight. They thought that should be doable. Will come back to this project and do more tests probably at that point. I guess I could always look into php myself but it does not fill me with joy. I'm hoping Max implements it, then I could add in documentation and run some tests.

Next I researched the [Picotron fantasy workstation](https://www.lexaloffle.com/picotron.php) to see if I wanted to purchase and play around with it. I found some cool projects, checked out the terminal, API, ran some programs online. Ultimately, I didn't find something to excite me enough to work on, so I'm going to pause on that for now.

Next, I worked on a web project. Some colleagues are in an exhibit opening in a month in LA and need a timebased 24-hour work to display in a website, updating once a second, as part of a show. Consider it something like a 24-hour long video with a framerate of 1 frame per second. They asked if I could make it happen. I developed a simple system and implemented a test, building out a simple site for them to check speed, image resolution, and for us to do some testing for robustness. Took me an hour or so for the initial test from idea to coding to deployment. Sent it along for their feedback. I should ask them for some money. I'll track my time. :)

By the way, this mini blog is being implemented in pandoc with front matter holding the title and css filename, and then just using a simple incantation in the terminal to render md to html.

[↑top](#)
