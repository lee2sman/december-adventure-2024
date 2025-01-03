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

## Dec 3

Much of the day has been consumed by me sitting on a couch with a laptop open and trying to crank out a professional document I have agreed to write, outside of my job but in keeping with the expectations of academia, to support faculty at another institution. It is not due until next Monday but the institution keeps asking me for it, so I'm trying to knock it out. Unfortunately it's been to the detriment to finishing up squashing bug on panblog. 

Anyway...I did get some time to work on it. So far I removed some old build scripts, tested my non-post page generation a bit, then added in some build automation to include opengraph (og:meta) tags, though ran into some issues when trying to populate the opengraph tags. 

Next I spent some time researching both metadata and front matter [variables](https://pandoc.org/chunkedhtml-demo/6.2-variables.html) in pandoc, with the goal to automate pulling a og:image url from frontmatter . I think I found a solution through the `--metadata KEY[=VAL]` option or the front matter, and finally found a [good explanation on stackoverflow](https://stackoverflow.com/a/26490978), that I think will be useful and I plan to use that to try to knock out remaining needs for populating variables. I also see useful info in the extensive man page `man pandoc` in the TEMPLATES section and then in Conditionals, which I think will be useful for testing if an image is set and then assigning the og:image metadata if it is.

Lastly for panblog, I began to rework gmi.css to an alternate "good defaults" new theme to ship with panblog. First, I checked out [2-color palletes](https://lospec.com/palette-list) from the Lospec website, and began trying some options, building out a new starter theme fresh.css.

Also, separately, I squashed a bug on [Archiving Artist-Run Spaces](https://leetusman.com/archiving-artist-spaces/) and added a redirect to my main/portfolio website in the /projects sub-directory in case anyone tries to manually go there directly (instead of to a project directly) so they are re-routed to root, which is the actual portfolio landing page, instead of a 404.

## Dec 4

Today I had meetings and taught my Programming Games class. Next week is the end of the semester so today I made a playtesting/coding day and the Learning Assistant and I went around meeting with students to help them squash bugs. We also talked about difficulty in games and tuning your game mechanics, and looked at examples of that across a few genres. The student projects are generally pretty great. I gave them the option of using Pico-8 or Love2d so there are lots of different kinds of projects, from platformers with bizarre mechanics, to race games, to experimental first person adventure stories. The biggest challenges my intro students deal with are writing collision detection for enemies, hazards, pickups, etc. The biggest challenge my advanced students have is reigning in their ambitious ideas that would take months of work and helping them shape a smaller, more doable multi-week project with the time allotted. I don't want to punish them for being ambitious, so usually I'll see if they can make just the first level, or a smaller component of their more ambitious game idea. This is especially important since they don't know to playtest and iterate and would tend to work in their head and solo until they finish, delivering a complete game before ever having another person try it out.

![the Purchcade arcade cabinet](assets/img/purchcade.jpg)

One of the senior students needed some extra credits so I asked him to work on a project this semester to build out a "bartop" arcade cabinet for student games. He made it out of plywood I purchased from the hardware store, and we ordered buttons and a controller from the internet. Then we raided my office stockpile of dumpstered keyboards, mice, monitors, etc that I've scavenged over the years, and used a Raspberry Pi from our spring [Special Projects in Tiny Computing](https://leetusman.com/tinycomputing_spring2024/) class. He installed RetroPie and Emulation Station and brought the nearly-finished machine, but we need to install Pico-8 and get EmulationStation to play it. I followed a [tutorial of sorts](https://www.reddit.com/r/RetroPie/comments/lurmu0/pico8_in_retropie_easy_uptodate_tutorial_with/) I found on reddit that seemed fairly comprehensive. First I had to escape out of EmulationStation and boot to the console. Hooking up Wifi on campus is a tedious process on campus involving registering the machine, visiting Campus Technology Services and the like. Rather than deal, I just plugged in directly to an ethernet port and got internet the ol'-fashioned way. I updated the computer, which took 15 minutes on the Pi, and then installed Vim so I could edit files. I downloaded some helper scripts from the tutorial onto my own laptop and installed them on one of my server spaces, then used wget in the terminal on the Pi to download and place them in the right places. I need to figure out how overscan works as I can't see the edge of the screen and thus it's hard to edit in the terminal. I don't have a regular GUI installed and didn't feel like going through the whole rigamorole to get that going, so I did my best to edit and tab around to see what I was typing, but mistakes were made! Eventually, all was well and I got Pico-8 to boot up. I couldn't quite figure out how the student had configured the controllers and they weren't working as I expected, so we'll plan to meet up tomorrow to try to finish up the controller scheme.

Finally, to procrastinate on finishing up the colleague review letter I worked on panblog a bit and continued hacking on a nice starter css theme for blogposts and index pages. I made a little test trying out a modification of a basic theme I started for a class website I taught in the spring. It's probably a bit "too much" for the out of the box theme but it would be nice to ship a few themes that are basically tiny css files since I feel most static site generators add that extra friction that you need to find themes and configure them when it could be as easy as just changing a single theme name in the front matter of a blogpost or page.

![testing out my theme](assets/img/fresh-test.jpg)

## Dec 5

Had our next-to-last Programming for Visual Artists class today. I showed students how to use CSS to affect the canvas, and how p5 fits into the rest of the browser ecosystem. I also showed them Processing in more detail, and when and how you may want to use it. For the rest of class students were given time to work on their final project due next week so I did lots of 1-on-1 meetings with students, debugging, talking through coding and conceptual ideas.

After class I met with J to get the controllers working on the arcade cabinet, which involves a lot of Bash scripts, configuration files and physical hardware. First I quickly cleaned up through a Bash script and some config files how Pico-8 works through EmulationStation. This will allow us to use EmulationStation as the back-end launcher so that in the future we can launch multiple game systems, and no keyboard required. Then we thought we were on a streak but we ended up spending 3 1/2 hours trying to get the darn 2 player joysticks and buttons mapped to the hardware correctly. Unfortunately we kept having weird problems like left/right being up/down, then we had left and right switched. Then we tried to fix it and I kid you not, the A button was now right joystick, seemingly at random. What a nightmare. The only good guide to configuring controllers we found and that seemed to work was on the [BBS forum](https://www.lexaloffle.com/bbs/?tid=38841). But eventually J found that a wire had fallen off the controller, and after reconnecting that, it solved one thing but we found we had other problems. We tried switching out controllers, swapping cables, un-connecting and reconnecting things, but each solution seemed to cause problems elsewhere. We guessed there is an intermittent short somewhere but lacked the energy to keep going because at that point, we'd put hours in and our brains were getting tired. So after all that time rather than leave defeated we got single player controller to work and will just have that mode ready for next week during final game presentation and arcade night, as I don't have time to work at school on this til the day of presentations. During the winter or spring we'll meet up again and try to get the second player controller working, and finally install the machine in the Lab. I'm a bit disapointed we aren't finished but it will be okay for next week because I think everyone turned in solo games for the Pico-8 assignment.

Aside from coding and teaching I also spent about 2 1/2 hours on the train and at home polishing up my letter of recommendation for a colleague and submitted it. I have to do 3 more (but easier) ones tomorrow!

## Dec 6

I think I got 90% of the MVP for panblog static site generator done. It's working well now, and I think the main thing left is to add correct OG:meta image variables and some project documentation, then start using panblog. What I have is a static site generator similar to others such as Jekyll and 11ty and Hugo, but simpler, with less variables and dependencies and the like, but fast. There is a single config.conf file where you put metadata such as website title, assets folder, site output folder, themes folder. There is a templates folder holding the site landing page and individual posts html template files. There are templates for header.html and footer.html files. You add posts to the posts folder in YYYY-MM-DD-name.md format, and use a standard markdown with frontmatter template. Images get checked in an images assets folder and on a post page you just write the image filename. After putting your post pages in the posts folder you just run the build.sh script to build the site. That's it! It's late so will have to get back to it tomorrow perhaps to finish the final details, but the todo seems not so bad: populating Opengraph image tag via frontmatter (might be tricky, hopefully not), adding conversion of non-blog pages (trivial), and then adding some documentation (fun). Finally, I'll want to see if I can build all my spring class websites using it quickly (3 sites). At some point I'll hopefully add in an image gallery template page and a project page template page as well from my website portfolio. Feels good getting to this point, and it uses knowledge I gained from my December Adventure time last year, then building the Archiving Artist-Run Sites project site and my website this summer.

## Dec 7

After a fun day out at the orchestra, then to see some sound art, then to dinner in Chinatown I came home. My partner wanted to see a movie I wasn't keen on so I put a few hours into panblog. It feels pretty close to completion for an alpha release. First, I fixed a number of bugs. Now, frontmatter is entirely optional. By default, the filename (e.g. *YYYY-MM-DD-a-title.md*) will be tokenized into a title and date, and all posts use the default site theme css file specified in the config.conf file. Optionally, other things can be set in the front-matter including: post title, theme to override the site default theme, an opengraph image url, and an opengraph description. Later, I may also add categories too and make an optional category page. I don't think it would be very difficult but I don't know if I need it, so maybe won't worry about that for my alpha release. Annoyingly, I spent over an hour or two trying to implement frontmatter custom variables with lua filters, bash, and then finally realized they're already implemented! It's just not well-documented in pandoc docs and I figured it out by perusing Pandoc's Issues on GitHub that they are already implemented and I just needed to use special syntax within my custom templates. I've updated my TODOs and see that the main thing left is testing: check that the RSS generator is generating a good RSS page; check that the rendered websites all work (need to try with other test sites). There may be a need to minorly debug the images asset folder if switching from title/index.html permalink to title.html. Speaking of which, uh oh, should I actually place all posts into an output posts folder? Otherwise they'll clog the output rendered site root directory. This would move them to _site_folder/posts/post_name/index.html for each. Well, I'll have to run some tests and see. Basically, I'll try to do a few tests on my own of these issues, make some sites, then announce and see if friends will test as well. I'm feeling good about where I'm at on this. It's at 99% of what I currently use Jekyll for.

## Dec 8

As I woke up this morning I dawdled in bed and read other folks' logs of December Adventure. From there I sailed from link to link and eventually landed on the blog of someone writing about Hugo, and then linking to its [quickstart](https://gohugo.io/getting-started/quick-start/). Let me apologize to Hugo that I now see the Quickstart is mostly straightforward and if I had seen it the first time without the ananke theme added I might have made a different choice just to go with it. For example, [smol](https://themes.gohugo.io/themes/smol/) theme seems to have 90% of what I'm looking for and no CSS pre-processor. It includes header/footer template code, though I'm not sure what calls it. And it's missing RSS, which I'm guessing is a tutorial somewhere else. So overall, a tutorial for Hugo quickstart but using smol theme and RSS, and some explanation or simplification of the header/footer would get to about where I'm at. It also has tags. I am far enough along that I'm not going to turn back now, because mine feels fairly feature-complete and mine is 200 lines and hugo, who knows, but probably in the tens of thousands of lines and a dozen or two build files. In any case, the advantages of Hugo within my own areas of focus: the option of mega more add-on features from external add-ons (though this is where things tend to get complicated, in my experience); an executable hugo file rather than pandoc being update via package management for example; image processing (to webp) in the extended edition, whatever edition means, though I could add imagemagick for processing easily. Okay, last I'll mention of hugo for now. 

Next I worked on my RSS feed generator. By the way, I'll bookmark this helpful stackoverflow answer on [yaml metadata in pandoc](https://stackoverflow.com/questions/26395374/what-can-i-control-with-yaml-header-options-in-pandoc) as its key to how I'm doing templating variables in panblog. When I need to grab a variable outside of a template I am using grep, like this:

```sh
# check if file has optional title in frontmatter
post_name=$(grep -oP '(?<=title: ).*' $file)
if [ -z "$post_name" ]; then #no title given, strip from filename
  post_name="${file_name//-/ }" #replace hyphen with space in name
fi
```

Next I ran tests on my RSS generator and though it validated through the w3 validator I thought I'd tweak it a bit. I pull in the title name or generate from filename, using code similar to the above codeblock. Then I added in guid for each post for best practices, but it's the same as a post url. I examined my generated rss file and it looked good. Then I ran it through the w3 validator again. All appears good.

![RSS feed validator](assets/img/valid-rss.png "Official RSS feed validator certificate")

Then I took a good long break and biked to Pioneerworks for the Press Play fair. Easily a couple thousand people there. I bought a sticker and some zines and mixtapes, and ran into a ton of friends. I saw Sam and Tega's open studio and caught up with them on Solar Protocol and their current projects. At night I came back and decided to fire up panblog to build a site. I started by copying my previous course website for Creating User Interfaces, which I last taught 2 years ago and have to teach this coming spring. It was easy to get the site up. I added in empty directories that panblog requires, posts, themes, templates, images; then copied over the build script, config.conf, and a css theme. I edited config.conf with my site URL, title and theme. I moved images over to the images directory. I edited the header and footer template lightly, changing out a line. Then I played around with CSS, and then...moment of truth...fired the build script up. Lovely! It works the first time! Fast. I noticed a minor bug, that the header wasn't included on the post_template and I fixed it on this site, plus went back and fixed it on panblog too. I decided I wanted the posts on this site to render from oldest on top to newest at the bottom, so I followed my own instructions to uncomment that option on the build script and commenting out the other way. It worked like a charm. 

Then I played around with the CSS, running build each time I made a change, and it worked fast and easily. I'm pretty happy with how everything turned out. See below pictures of the render site. Note: I added a drafts directory and moved all of the posts except for week1 into that. The drafts folder has no bearing on the rendering, so it's a fine way to hide stuff for later. Idea borrowed from other static generators. I'm not implementing something like "--build-drafts" or whatever. I never use that since it's easier to just check into posts folder when it's ready to test and build.

![Creating User Interfaces class website test](assets/img/cui-site.jpg "Creating User Interfaces Class Website test, with image of soviet interfaces")

![Interfaces page - week 1 of class site](assets/img/interfaces.jpg "Class Website with text and image of Soviet census computer")

I'm feeling pretty great about this. I'll come back and do another site test for something different later, then announce and get friends to try it out, and then spread the word. It's great I've built this tool, something I've felt I've needed for years. Goodbye Jekyll! (Well, except for the two big projects I've built that rely on it and I'm not sure I want to switch them now because they rely on Liquid Templating. But one day, if I have to!)

## Dec 9

Today I prepped and pushed a v0.1alpha release of panblog. As it's pretty late at night, I'll try to announce to friends starting tomorrow and see if they want to try it out. I've also published a [demo site](https://exquisitecorp.tildepages.org/panblog-demo/), built using the the panblog repo "out of the box". In prep for that I pushed some fixes to build.sh, cleaned up the css template, and updated the demo posts with some additional text. Then I spent a little time reading up on hosting via [tildepages](https://tilde.wiki/Tildepages). It was pretty easy, but I did post the site to a separate repo to keep my original panblog software and the output separate (and because the panblog repo pushes the site to _site folder and I don't see a way on tildegit to specify a subdirectory the way you can on GitHub pages).

Earlier in the afternoon I worked on the timelapse website for my colleagues and built another test page for them to check out. It's like a very low, very slow flipbook, one image a second, all day, of plants germinating, growing. I will be taking a 24 hour video, converting it to still images, one per second, pegged to the exact hour:minute:second in the day. I decided to do this with front-end only and implemented an async promises approach to image-load. I don't have any previous experience with promises so looked at some examples and then tried to implement the idea myself. I used test video rendered to stills via ffmpeg for the test site I built. Now that the test site works the next step is to build the final site. I'll need to grab the huge multi-gigabyte video file and chop it up through ffmpeg and name the files based on HH-MM-ss. I may need some shell scripting to output each frame with the correct filenaming schema. Then I'll have to modify my code a bit. Finally, there is supposed to be a poem, some overlaid text on top of the image files so some CSS wrangling for that, especially if the site needs to work on mobile. I think I'll get back to this project next week after the semester ends.

In the evening I went to one of the book release events for Nick Montfort and Lillyan-Yvonne Bertram's (editors) anthology book OUTPUT which is a compilation of generated texts spanning from 1953 - 2023. 

Tomorrow I need to get back to working on the computational art website Random Walk that I'm building out with student artwork.

## Dec 10

A little coding today. I was working with a student on a project and we needed to figure out a flashlight-type effect where moving the mouse around illuminates hidden items in a dark scene. I tested out the mask procedure that's been added to p5 since I had last checked. But the way it works in an additive fashion didn't mesh well with how I was approaching it at first and I couldn't immediately get the specific result I wanted to get. So I quickly plunged into a bit of a brute force approach and I figured out a fake masking effect by creating a black opaque image twice as wide and twice as high as the screen dimensions, with a transparent circle in the center. This gets centered and drawn on screen at the coordinates of mouseX,mouseY. Moving that around as the player moves around illuminates the scene. Optionally, I could have the whole scene covered in complete darkness and switch to the one with the hole only when pressing down the mouse. I don't know if I'll need this again but it was a fun little test.

![Random Walk screenshot](assets/img/random.jpg)  

In the evening, I prepped the [Random Walk](https://randomwalk.club/) website to be ready for public release. Random Walk is my now online journal of computational art, inspired by [Taper](https://taper.badquar.to), [Oral.pub](https://oral.pub/) and the [HTML Review](https://thehtml.review/). In the first *issue* of Random Walk I published work from the students of my intro course Programming for Visual Artists. This is a class for students with no previous background in programming. They get a math credit, and I teach them how to make art with code. Of course we do cover all the basics from variables and functions to loops, conditionals, arrays, and objects, a graphics pipeline, working with media and sound. All that and fluxus, Yoko Ono, to the experiments at Bell Labs, to early net art and contemporary new media artists that work with code as medium. The idea for the online journal came to me last month when the students were giving presentations on their work and I was impressed by their work and what they had to say about it. I thought creating a website inspired by these other online journals could make a nice framing device, and I coded up most of the site around the Thanksgiving break. As well, I hope this site provides me some flexibility for future online computational art issues, perhaps from my Purchase College community, or perhaps beyond.

## Dec 11

Most of the day I was at school. I had a meeting and then set up and then an end-of-semester games night where we showed all new games by students in my intro Programming Games class and the upper level class Experimental Game Lab. At first I didn't think the students would show or that we'd have much of an audience. It was pouring rain all day. But the students did come, they set up with me, put out their games in an arcade-like arrangement I set up. We also revealed the new game arcade cabinet made by the senior doing an independent study with me. I was able to get some funding to order pizza and seltzer so that was nice to feed everyone. It had a arcade-in-the-art-gallery feel.

In the evening I wasn't sure what I wanted to work on so I re-read my week 1 notes and decided to pick up working again on this 3d webgl project. I don't fully have the language for it, but it's intended to be something like an experimental narrative work to present in an exhibition. I have a 3d model of a head I built out of basic shapes and some objects in a WEBGL environment I coded in p5.js that I coded about 2 years ago for an exhibition. I went back into it and turned it into a class so I could make several heads, at different points in space, with their mouths synced to different playing audio. I have drawings as textures on the models, so the head is a psychedelic-looking digital avatar. I have recorded an interview with my mom after Thanksgiving: a conversation on the family history of our name, which functions as a conversation about assimilation, feminism religion, culture, values and family. That's a ton of issues tied in, and it's why I wanted to work on this for a long time. In the next few days I want to get a prototype up of our conversation, with our digital heads speaking our recorded dialog to each other. Where our heads are made of my drawings, but of what these drawings should be, I'm not at present 100% sure. Our digital lips, which I created from torus shapes, sync with our dialog. I would have preferred to port everything over to Love2d but I wasn't sure if it'd be too much effort. I realized tonight as I was wrapping for the night that I should check out [g3d](https://github.com/groverburger/g3d) (groverburger's 3d engine) a bit more and decide whether it could work or if I should continue with p5.js or maybe Processing. I don't think I'm making a web-based work, so a stable desktop environment would be preferable. Also, the browser is sometimes having a memory error. I don't know if it's because of the size of the audio files I'm working with, and those could probably be cleaned up, or a 3d model/texture issue from WEBGL. I'll have to look more into that potentially. But I bet Processing or Love2d wouldn't have the same issues if it's a memory issue. Anyway, something to work on. An art piece to explore. That should be a fun for me, as I have enough of an idea to spark some experiments, but not all the pieces yet.

## Dec 12

I taught my last class Programming for Visual Artists for the semester today. Students gave presentations of their final projects. Some of them were really great. Most put in good effort and made work to be proud of. We did a critique that took a few hours, and said our goodbyes. I'll see them in the spring.

At night I put in a little time checking out the g3d library for Love2d. I downloaded the demo scene and it runs straightup and the code is clear. I tried importing the objects (hair, traffic cone) from my p5 project I worked on last night. I couldn't get it to run. I went to the g3d wiki, which is pretty short, but it clearly says I need to export the obj objects as "triangulated" and suggested I use Blender to export it. It's just a simple checkbox. I wasn't sure if I needed to rotate or scale the object and just left the defaults for now. I then imported and found it worked. It helped that I was basing things off a 3d model of the planets and I'm trying to make a round head.

Here's a screenshot of hair, textured with my digital drawings, floating at an angle in space! I'll try out more soon.

![hair flying in 3d space](assets/img/hair.jpg)

## Dec 13

I did not code today but I thought about coding. Instead I did some school work, got a covid shot, and went to a magazine release party/performance/reading and then a party at a friend's loft. I got home and didn't feel like coding and instead listened to field recordings / experimental music on [Biesentales Radio](https://cashmereradio.com/shows/biesentales/) / Cashmere Radio. I thought about my experiments with g3d yesterday and currently I think it probably makes the most sense to keep going with its p5.js incarnation that I already started first, rather than try to port the thing to Love2d and get stuck in the weeds. What I'll probably do is keep working with the p5 project as is and complete the initial idea in my head, since it's not far off. Treat that as a prototype and see if the story and project feel like they're working out. It may work, or may need more attention. I can experiment with the drawings wrapping around the head of the charaters, with a random-path narrative, and try out moving the camera, etc. I need to see how WEBGL works or if it crashes too much with my files. Then I'll consider if its needed to port to Love2d, Blender's [UPBGE](https://upbge.org/#/) game engine (that [Danielle Brathwaite-Shirley](https://www.daniellebrathwaiteshirley.com/) told me she uses and likes), or maybe Godot. Hmmm. I also want to play with Pure Data/Plug Data, and play more modular synth, and work on Solar Sounders with [Daniel](http://dfiction.com/). And the handheld PockChip. And my podcast! So much I can play with during the winter break. Ok, going to go read in bed.

Coming back a couple hours later. I tried setting up the [Swords of Freeport](https://swordsoffreeport.com/) door-game/MUD-like on the tilde server. I hope I set it up right for other players. I tried it myself and played for a bit. It's fun.

## Dec 14

I checked out [Seamstress](https://github.com/robbielyman/seamstress) art engine, which you program in Lua, and uses Love2d, Zig and Lua under the hood to allow the user to program small art and music sketches, kind of like little guitar pedal effects and patches I think, but the workflow seems to mostly revolve around Monome Grid or midi, neither of which I use, and I couldn't find any other starter code. I moved on and checked out [yabasic](http://2484.de/yabasic/), and I like how flexible it is. I don't immediately have a project in it, but I was looking around for FutureBasic (which I purchased for my birthday as a kid) and was looking into whether there were any Basic variants that allow functions, for example, and came across yabasic. It's modern and minimal, cross-platform, and includes visual libraries and socket libraries, so this could be something cool to work with.

Then I spent time working in audio editing to prep for integration with my p5.js code. I need to separate out an interview I did with my mom last month into separate voice tracks. The audio source is only about 20 minutes long, so I decided that rather than edit, since I didn't know what *shape* things will take, I would first just try to test how things/look sound when the audio and visual sketch are combined together. To complete, I first duped the audio and used audacity to cut out my mom's voice from my own audio track and exported it. Then I began work to separate my voice from my mom's audio track. I didn't quite finish yet, probably tomorrow. Now I have to head to the rhizome fair and then the sauna night and holiday party at my art collective, so probably no more code or project work today.

## Dec 15

Today I got back to working on the project in p5.js. When I cut off yesterday I hadn't yet solved an issue with detecting volume level separately. I always advise my students to pull out the problem section of code and try to isolate it and debug it. So I did that, and showed my partner. And talking it through together and looking at the old p5.sound reference I found I was using the wrong method to set the amplitude. Well with that knowledge I made a successful [test p5 sketch](https://editor.p5js.org/2sman/sketches/llqCyQB27) through the web editor to demonstrate tracking two different voice files. So now I could apply that to my main project and quickly had success of a sorts. 

![screenshot of early demo of "hyphenated heads", in p5.js/WEBGL](assets/img/heads.jpg)

I got to a first test point. I have two heads load, and they start to have a conversation. I don't think it's particularly visually compelling or a complete anything yet, but here's my open studio and you're poking your head around checking out what I have piled up on the floor. Here it is. Oof, must have audio capture mis-configured. It sounds like I recorded audio routed out, captured back in by the mic! No idea.

The conversation is one I recorded between my mother and I a couple weeks ago. I interview her about our family name, why we changed it, and intersections with our culture, feminism, and equality. This demo capture below is just the first half a minute, while I'm testing moving the camera around. The background is blank, and our heads are fairly simplified. I think all of this will change, but it's meant to be a start for me to evaluate whether this is even fruitful to pursue as a project I envisioned in my head originally about a year ago.

<iframe width="560" height="315" src="https://www.youtube.com/embed/En5UJmZsPU8?si=jEdWXgBfGu90XAd0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

I watched for a while. I need to do some minor audio edits but Audacity glitched out. I think my running the sketch takes up lots of memory. I need to look into it further. But I'll say that my thought that this is a compelling approach to telling the story seemed to 'work' or at least seemed like a promising approach. But having just the lips move and occasional eye movement is missing some of the 'natural' feeling needed. The heads are fake but with the recorded voice it approaches an uncanny valley. I added in occasional head tilts a bit, because we're missing the natural body movements with the floating heads without bodies. This helped a bit. I'm wondering if next I should add in something like the TV style 3 camera approach, strait ahead, 2/3 view, and entire scene. I also wondered if the heads should be looking at each other directly or if this angled for an audience view worked better. When I interviewed my mom I looked directly at her. When I interview for a podcast in person we sit at an angle together. Maybe adding switching camera views could add something. Perhaps even looking out from someone's eyes. I am also confirming the background blank doesn't work well. I want there to be a complex, changing background. I'm worried I'll run out of memory and should have moved to Godot or Love/g3d. In any case, things are moving forward and I like the approach.

## Dec 16

More work on the "hyphenated" project. That's just a working title. I added glasses and eyebrows. A more normal person would sculpt this but I made it out of 3d primitives (torus and cylinders) and a ton of rotation and translation commands. A bit goofy. A dozen or two lines of code. And lots of experimentation to get angles and such right. But it works. I also did some tests trying to add in occasional eyebrow movement. For example, I mapped louder volume levels of my voice to trigger an additional rotation of my eyebrows upward for a split second. But I couldn't quite get to anything that looked visually compelling. I had these little glitches get introduced and my mom's head disappeard. I might come back to that. Next I spent some time looking for some patterns to wrap around the heads and use in the background - specifically early cultural wallpapers, blockprints and other patterns from early yiddishkeit community in NY, looking on the New York Public Library site and some other archives but didn't find what I'm looking for. I was thinking I could make a simple panning background like I did for the [bokjoy](https://leetusman.com/bokjoy/) performance toy I made for the Roots Studio fashion show in the spring. I'll need to spend more time during my winter break investigating image sources. I'm wondering if I want to connect this small-ish story piece to the idea that the word glitch potentially comes from [early German or Jewish immigrants](https://en.wikipedia.org/wiki/Glitch#Etymology). If so, switching between old prints and patterns and then 'glitch' aesthetic might be a nice addition.

![glasses on my avatar](assets/img/glasses.jpg)  

## Dec 17

No work on my own code today. Had some appointments, and grading is due tomorrow. 

## Dec 18

Finished grading today. Two holiday parties tonight. When I got home I worked on the website project for my colleagues that have an exhibit. The website loads a new unique photo every second for a 24 hour cycle of blooming flowers. I wrote the image loading script earlier this month on the 9th. Today I worked on creating and styling the modal, and then ran a test. Since it was after midnight, I immediately noticed a problem: the generated images from the movie source count like this: 1, 2, 3,...10, 11, 12..100,...etc. But the files are name sequentially like this: 000001.jpg, 000002.jpg, etc. This is trivial to do, but it still requires doing! So I wrote in this code to convert seconds to this proper filename if the time is less than 5 digits in length and voila, a first test done.

## Dec 19

Some experiments with the narrative piece today. I added ears, trivial. But then I also tried searching for and changing out images, both the texture on the heads as well as adding a scrolling background class. I need to do more work on the scroll, and the images DO NOT WORK WELL and I really need to find others. I am not finding exactly what I'm looking for, but I tried some things from the Metropolitan Museum of Art's online collection. I'm looking for patterned, woodblock prints and the like, textures, paintings, other things from 1900s jewish immigration period, but that's hard for me to look for online, and I think I'll need to visit a library or special collection to even begin to find useful things. I'm thinking I may try the New York Public Library next. 

## Dec 20

Was out most of the day and away from computers. Spent a little time before bed working on the background scrolling technique, making it more efficient. Didn't finish but figured out some bugs.

## Dec 21

Wow, a great day. In the morning I started the process to set up a research consultation at the New York Public Library and specified the kinds of patterns and photos and prints I'm looking for, and to check out the [Dorot Jewish Division](https://www.nypl.org/locations/schwarzman/jewish-division) of the library. I have an appointment booked in January. 

Then I took a solo trip to MOMA, joined as an artist member, then had an incredible time walking around and seeing art. Highlights included seeing Van Gogh's Starry Night, Rafael Rozendaal's large projection of Css (and JS) works in the lobby, Christian Marclay's The Clock, and so much more I obviously can't describe them all (Pollock, Warhol, new contemporary installations, John Giorno's Dial-A-Poem, Nour Mobarak's great audiovisual installation, Robert Frank's video scrap files, Matisse's paper cuts...). 

I think seeing the Romare Bearden [patchwork quilt](https://www.moma.org/collection/works/79986) collage work today, along with the other video and art installations might have inspired this idea. I'm not sure. But I came up with this idea of using my [NaNoGenMo quilt poem concept and code](https://leetusman.com/nosebook/quilt-poems) to create new quilt-patterned photo grids using my photography archive. I had to rewrite, used some old code, but in the end it's only about 50 lines of code or so, save for the quilt pattern encodings as data. This is just a first iteration but I'm already kind of pleased. It pulls a random quilt pattern, then 8 photos, resizes them to a standard block square size, then builds the quilt according to that pattern from the quilts.lua file. 

![a "little coins" quilt arrangement](assets/img/quilt1.jpg)

![a "drunkard's path" quilt arrangement](assets/img/quilt2.jpg)

After coming up with the idea but before I coded it tonight I had dinner with an artist friend and talked about how excited I was to execute the idea. I began brainstorming some future ideas and iterations, which has turned into these following ideas I may want to try going forward:

* pick a random quad from the photo rather than resize whole photo source
* pan and scan over the photos so they are moving?
* some photos and some plain color fields?
* do videos instead of or in addition to photos? i guess that'll start looking like a nam june paik.

I'm not sure the meaning of the work or if it will stay purely abstract at this point but it's feeling fruitful. I think personally without a broader social or even basic concept I can't get to a point where a piece will feel complete. I also wished this would be useful as background for the other work, the interview piece with my mom, but I don't see a connection here yet. In any case working in Lua/Love2d is a nice and intuitive process for me now, even as I still rely greatly on the reference. I enjoyed my coding tonight. I have a [code repo](https://tildegit.org/exquisitecorp/quilt-photo-grids) for the work in case I keep going with it.

## Dec 22

I'm having a lot of fun working on my quilt variations. Yesterday I had the the photo blocks consisting of resized photos squished into the size of a block. Today I modified the program to pull random quads from the photos instead. So the images have gotten more abstract, but more interesting. Still, I'm producing abstractions and even more Nam June Paik-ish work. These are with still images. Maybe next I can try the 'pan-and-scan' approach and then video?

![amish bars quilt](assets/img/amish-bars.jpg)

![little coins quilt](assets/img/little-coins.jpg)

![Drunkard's path quilt](assets/img/drunkards.jpg)

![Checkerboard pattern quilt](assets/img/checkerboard.jpg)

I have a bit of a memory issue I think. After generating 15 quilts every time there is a crash and my program errors and quits. I'm assuming the images are loaded in memory and not overwriting the previous. In Javascript I think it would just overrwrite but I guess I'm not understanding in Lua what it's doing on the back. I need to read more about memory and images and see if I can fix this in the future.

Coming back several hours later and a stranger on an internet forum is trying to figure out the memory issue with me. They made some suggestions but each of these didn't solve it. 

Meanwhile I posted that my fave music from 2024 is the A. G. Cook track [Silver Needle Golden Thread](https://www.youtube.com/watch?v=GWAocs5P0no). Someone directed me to the music video for it, made by artist Lena Weber ([great interview about the piece, coded in python](https://timrodenbroeker.de/lena-weber-ag-cook/). I realize that my quilt-maker could be in this line, but the memory issue is preventing this. 

Meanwhile I spin up another Love2d test file. Now I practice drawing images to an offscreen canvas buffer, then pan across that buffer and draw a section to the screen. This is my test of drawing panning/scanning images. First test passes. I may try to integrate this into the quilt pieces.

## Dec 23

Wow, wow! Thanks to a stranger for chatting with me online on the Love2d reddit. They tested the garbage collector and that single line added prevented the memory errors. So I added it to my code, and boom, it works! No crashes. Another person suggested the canvas drawing approach was a good one to speed things up as well. So I'll use my side code from yesterday and probably integrate that in as well if I want to make this 'music video' speed. I could also likely run the garbagecollector somewhat less often and do some tests, instead of every new quilt, maybe every 5 for example. I've already shot some video using this v1 of the software. It's working well. I'm happy. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/s4I0x5bUnsg?si=UY3Ps7VhyYIcJvZx" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Later in the day, based on some suggestions from the internet forum I decided to try out drawing with the canvas functionality to see if there's a performance boost. So now I have implemented drawing the photo grid to an offscreen buffer canvas, then in the end of the draw() function I draw that canvas onto the screen render. I do think maybe there's a bit of a performance boost, but the speed doesn't knock us into fast frenetic music video speed yet. Maybe next I need to try some scaling and somewhat less frequent garbage collection. In any case, I still think I have a successfull first version of this project.

## Dec 24

I was away from my computer for the day/night so didn't do any coding. But I did read the bulk of [Output: An Anthology of Computer-Generated Text, 1953 - 2023](https://direct.mit.edu/books/edited-volume/5867/OutputAn-Anthology-of-Computer-Generated-Text-1953). I also read a bit some programming articles on my phone before bed.

## Dec 25

Got home pretty late. I had the idea to try out adding a first version of image panning to my quilt generating program. First I watched some examples of "the Ken Burns effect" on youtube but then realized I didn't need all that, just a simple pan. I wasn't sure at first how to implement it, but it turned out to be simple. Rather than choose a random starting x and y coordinate each time I draw a quad now I create an starting x and y coordinate for each quad in a table and just alter the x and y coordinates in the love.update() function. There's a slight "hiccup" each time a new quilt is assembled. I tried taking out the garbage collector and it is no slower, but also no faster. It doesn't crash anymore either. Maybe the new quad coordinates somehow trigger the hidden garbage collector to work? I really am not sure. Anyway, here's a simple test of panning:

<iframe width="560" height="315" src="https://www.youtube.com/embed/zmQ5-bJvEDo?si=7Y8c_MgKyLtnNMsi" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

I need to figure out where I want to go next with this project. 

* Should only some images pan while others are static?
* pan different direction (up, down, left, right) randomly selected at start?
* Should I play with scale and have each quilt have bigger or smaller blocksize?
* To the point: what would it take for this project to feel *finished*?

I am also thinking I may want to try making more intentional image sets: either use my ENTIRE travel photo set, or maybe just graffiti photo set (and why that?).

I wonder if I want to add modular synth music to this. Or maybe an audio interview or recordings on top. Or maybe...'procedurally generated' randomly selected audio clippets and maybe music.

I might need to put the project down for a bit and then come back to it and see what I feel compelled to do.

Later on someone asked me about the software on Mastodon and I linked them to the repo. I realized maybe I should add a license and like always overthought then came back to the ACSL license. The person asking about the software has previous experience in p5 but not Love so I pointed them to my tutorial [From Processing to Love](https://github.com/lee2sman/processing-to-love). I added some additional notes on seeding pseudorandom numbers in Love, and async/sync differences in p5/processing/love.

## Dec 26

Today I visited the New York Public Library. I had an appointment with a research librarian at the Gregorian Center for Research in the Humanities to help me with some research in the Dorot Jewish Division. I am interested in finding some resources that might inform the piece I'm working on currently, that consists of a conversation between my mom and I, and wanted to see if I could find any sources that might inform my work, or might be useful visual images to incorporate into the digital construction. After getting a thorough overview of research sources and databases I browsed various digital archives and then requested some old cookbooks for on-site research, thinking that they may have imagery that might potentially be useful to me. In the afternoon I worked on editing and cleaning up the audio interview source a bit. Later I did a bit of work with in code cleaning up the background scroll, and adding in the new image sources from today at the library. While the images don't feel like they cohere yet, I think it feels like it's cohering around the original vision I had in my head. I'm feeling like it's time for "studio visits." I'm going to show my family when I visit them this weekend, and I think I'll set up studio visits with some artist friends to start to get some feedback to see what's working or not, and if I'm on the right track.

With just a few days left in December, I feel like this has been a useful month and gotten me on a good daily work progress. I hope to continue this throughout the year ahead, just as I used to do [everydays](https://leetusman.com/projects/everyday/) for a couple years and found them pretty helpful for advancing my programming as well as my art practice. Since I'm moving away from Javascript somewhat, and because some of these projects are 'larger', this journaling has been nice for the month, though I'm not sure I want to continue doing it to this frequency or amount of writing.

## Dec 27

I was out most of the day and night. Before bed I spent some time reviewing the LOGO language. I am teaching a course in the spring where I covered LOGO the previous time I taught it so I was wondering if I wanted to do that again. For some reason, I have been feeling less interest in LOGO lately, so I wanted to see if I could get some spark back. I decided to try a few variants that intrigued me and play with my own little PLOGO Javascript library as well. First, I read about [LibreLogo](https://www.stuestoel.no/office/logo/en/logo-startside.php). Did you know that LibreOffice is packaged with a LOGO variant, and that you run it inside a document? Weird! Cool that it's in LibreOffice so it's very accessible, but entering commands in the input form or running a page of a doc is a bit funny and I didn't take to it. 

So next I decided to try UCBLogo. First I tried the latest, which is on GitHub and was last updated yesterday! I couldn't get the configure to complete, commented out some tests that were throwing syntax errors (probably due to variations in versions?) and tried building. It builds but wouldn't run correctly. So then I decided to run the last version complete at Berkeley. When I did that, I had a choice of what to run, and I decided to download the last DOS version, and I installed via DosBox and it contains a couple versions but I could only get the oldest one on there BL (Berkeley Logo) to run, which is version 3.6. Ok, it's an old language anyway, that's fine. It's funny to me that I found it easier to install and run it on DOS than for my present OS.

The official [UCBLogo website](https://people.eecs.berkeley.edu/~bh/), which includes the downloads, is a wonderful example of a [Prof-Dr site](https://leetusman.com/nosebook/prof-dr-style) site by the way. I love it. I went through the first chapters of Brian Harvey's [Computer Science Logo Style volume 1: Symbolic Computing, 2nd Edition](https://people.eecs.berkeley.edu/~bh/v1ch1/explor.html) (available for download from the Harvey's UCBLogo website, published in 1997). It's the first of three books he wrote intended for both a general as well as a CS audience, and I enjoyed his writing style and emphasis on having fun and experimenting while learning the principles of LOGO and Lisp and general programming principles. Surprisingly to me, the books are NOT focused on Turtle graphics but on the principles of computing. 

Next I tried messing around with Turtle graphics as I remembered them. I wanted to draw a random quilt, which is something I have my students do, but I accidentally mistyped something and had a recursive loop. I enjoyed watching it draw for a while but I couldn't figure out how to pause or stop while in a running procedure so I had to eventually force quit because I didn't feel like waiting. And that ends my first day playing with LOGO.

## Dec 28

Today I went through the list of [LOGO software](https://el.media.mit.edu/logo-foundation/resources/software_hardware.html) on the LOGO Foundation's website. I tried out a lot of different web-based Turtle-graphics programming environments in search of one I'd like. Some are text-based and some block-based. All of these are intended for school audiences. Of the block based ones intended for young folks and a bit simpler than Scratch I liked [pencilcode](http://pencilcode.net/edit/first) more than [TurtleArt](https://www.playfulinvention.com/webturtleart/), though I do love turtleart's [reference guide manual](https://www.playfulinvention.com/webturtleart/webhelp/reference.html) is only 15 pages.

Out of everything I tried I think the Apple LOGO II from 1984 is my favorite, and works well on [Archive.org](https://archive.org/details/Apple_Logo_II) except that you can't save there. 

I didn't do a ton but tried out building some basic loops and functions.

![Apple Logo II](assets/img/logo.png)  

## Dec 29

Today I hung out with family and friends and barely put time to coding. I have just a few minutes before bed. I played in the browser with Pencil Code, a block-based editor like Scratch. I found that you could use the 'wear' block and type in a random word and most of the time it changes the turtle to that image.  

Anyway, here's a [random quilt](http://leeto.pencilcode.net/edit/first-quilt) again. This took very little time and is not written efficiently :) One thing I like about block editors is that you can generally instantly 'dump out all the blocks' like legos and see what commands are available. 

![Random color block quilt coded in pencil code](assets/img/pencilcode.jpg)

You can `click for text` and switch to text mode.

```LOGO
moveto -200, 200
speed Infinity
for [1..4]
  for [1..4]
    pen random color
    for [1..4]
      fd 50
      rt 90
    fill random color
    rt 90
    fd 50
    lt 90
  lt 90
  fd 200
  rt 90
  bk 50
pen white, 10
fd 50
```

## Dec 30

Same story as previous days: not much time for coding. I had a train ride though, and decided to work without internet. First, I spent some time reading Turtle Bunting: A LOGO Vexillological Reader.

<iframe src="https://archive.org/embed/peter-carter-turtle-bunting" width="560" height="384" frameborder="0" webkitallowfullscreen="true" mozallowfullscreen="true" allowfullscreen></iframe>

Then I decided to keep working on simple quilt algos. I used turtle.lua this time, a simple turtle programming library in Lua with the Love2d framework. Since I already like Lua and Love2d, this seemed the most natural to work in, but then you lose the advantages of Lisp and Logo. The turtle.lua library is a bit clunky. Like Love, I don't like having to call things like a class. I prefer p5-style or original LOGO style of coding. I recreated the quilt but then didn't do much afterwards.

```lua
--excerpt
function patch(_x,_y,_length)
  t:penup():setpos(_x,_y):pendown()

  t:color(love.math.random(255)/255,love.math.random(255)/255,love.math.random(255)/255)
  for fwd=_length,4,-2 do
    t:forward(fwd):right(90)
  end
end
```

![A quilt with random color blocks programmed in turtle.lua](assets/img/blquilt.jpg)


You see what I mean about it being a little clunky?

It is cleaner (to me) to write more like the following, though I need to check the way to work with parameters.

```logo
  setpencolor random 16 repeat :length/2 [ fd :fwd rt 90 ]
```

Today I also found [JSLogo](https://www.calormen.com/jslogo/) (see [code](https://github.com/inexorabletash/jslogo)), which looks useful for a mini 1-off workshop I may teach. 

<div id="current"></div>

## Dec 31

End of the month!

I'm having fun playing with LOGO the past few days. Today I spent time with LogoJS, by Joshua Bell, which implements a subset of UCBLogo and runs in the browser. It's really robust and full-featured.

This is definitely the best web-based LOGO IDE I've used, and I like it as much or more than the p5.js web editor I teach in my Programming for Visual Artists class. Click to see examples and it shows basic easy to read and use example code that you can send to the code editor. By default it saves all code you run in its history. You can also click to see the reference popup, click Library and it pulls up the code for any procedures you've written. Brilliant.

Here's a three turtle race, starting with some example code I modified:

```logo
clearscreen
setturtle 2 penup right 90 forward 100 left 90 pendown
setturtle 3 penup left 90 forward 100 right 90 pendown
repeat 200 [
  setturtle 1 forward random 4
  setturtle 2 forward random 4
  setturtle 3 forward random 4
  wait 2
]
```

I started reading the [Turtle Bunting](https://archive.org/details/peter-carter-turtle-bunting/page/n4/mode/1up?view=theater) workshop I wrote about yesterday. It is from 1990. I read the intro and did the first activity. The book assumes that you are using any of many versions of LOGO and will have to adapt the code for your version. 

> In a conventional programming book there would be discussion of the process of analysis, design, coding and validation, with pseudocode, structure charts and that sort of thing. In this book there’s very little of that (there’s some in boxes) and you will work in reverse: this is programming by example. Read a procedure, think about it, and make sure you understand it before moving on to the next.

So that's what I did. 

The book goes on:

> Aboriginal

> It’s perhaps fitting that this is the first flag in the book. A simple, bold design, it was first used in the early 1970s, and has become a readily recognised symbol of the aboriginal community’s struggle for rights and recognition


Here's my version of the Australian Aboriginal Flag:

```logo
to block :length :width
  repeat :width / 2 [ fd :length rt 90 fd 1 rt 90 fd :length lt 90 fd 1 lt 90 ]
end

to earth
  home rt 90 bk 158 setpencolor "red block 319 95
end

to sun
  pu home pd setpencolor "yellow repeat 720 [ fd 60 bk 60 rt 0.5 ]
end

to people
  home pu fd 90 rt 90 bk 158 pd setpencolor "black block 319 95
end

to aboriginalflag
  people earth sun
end

aboriginalflag
```

There are procedures for many country flags in the workshop, sea signalling flags to be used by ships at sea, and the Earth flag. Each of the procedures are written in a different version of LOGO. Some random ones I encountered: Logotron LOGO, Apple Logo, Atari Logo, Macintosh Logo, LCSI Logo, LogoWriter.

The workshop is pepppered with dozens of comments and questions like this:

> What happens when something we see or hear contradicts our mental models? What happens when the procedure we’ ve just written turns out not to do what we wanted? Is programming a model of learning? Do mistakes matter?

Well I have to go now to set up for a New Year's Eve party at our artspace. So this is my last official post for December Adventure 2025. I kind of tapered off at the end there, just doodling around with LOGO, but I had fun and I feel ready to teach with it. I think it will be a fun opening activity workshop in my Drawing, Moving and seeing with Code class, which I'm going to try to teach more like an experimental lab than an instructor-led seminar/studio class.

This month I coded in LOGO, javascript, Lua, Bash, HTML, CSS. I worked on some generative art, on a longterm ddocumentary digital artwork, on a static website generator, on a website for a friend's day-long slow film project, on documentation, and on little tests of LOGO. I didn't get to everything on my list to do, especially music. But I have a couple weeks more off school so will do more music and Pure Data next, and maybe get back to Pico-8 and continuing work on my documentary art project. I still want to try Construct 3 for rapid game-making, so maybe will give that a shot, and get back to my work in Forth. I'd love to make a version of LOGO implemented in my custom FORTH. Anyway, this was good to have a daily practice, and to log my work. I'll continue perhaps to do this kind of studio practice. I need to figure out where I should log about it, like a tinylog, and I probably won't do it every day, but will make it more regular. It's a great way to expand my skills and refine my artwork and craft. And it's fun, and great to look back and see what I've done. Thanks to Eli for starting the December Adventure series, and it was fun to follow along with everyone else this month. Cheers


[↑top](#)
