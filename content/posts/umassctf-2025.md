+++ 
draft = false
date = 2025-04-21T18:46:20-04:00
title = "UMassCTF 2025 OSINT Writeups"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

Now that UMassCTF 2025 is over, I think it's time to explain myself. It was my first time writing CTF challenges, and I think I did a solid job. I went in wanting to write challenges that were:
- Interesting and made you think a bit
- Couldn't be easily reversed image searched (since it's more fun when you have to work for the answer)

I wasn't able to write as many challenges as I wanted, mainly due to a lack of time in the weeks leading up to the CTF. The challenges I did write were the best of the ideas that I had. Without further ado, let's get into it.

## Attack of the Pentium 4
Story time: one of my friends was building a computer, and I was helping spec out his build in a Discord call. We were trying to select a case, and we both got sidetracked and fell down a rabbit hole trying to find the ugliest cases ever made. Eventually, I stumbled upon this [TechPowerUp article](https://www.techpowerup.com/51177/zeus-shows-off-usd-750-000-pc) about a company that had designed cases built out of solid platinum and gold for eye-watering prices. I knew I had to learn more, so I clicked the link to their webpage. Enter: Computer Zeus.

![Computer Zeus Homepage](/images/umassctf-2025/pczeus.png)

Computer Zeus is a Japanese build-to-order PC business. Their whole schtick is building PCs for clients who might not know exactly what they want in a computer, but do know what they want to use their computer for. Despite this, they have some strange configurations, [like this Core i5 14400 and dual RTX 4060 PC for ¥316,800 (around $2,250 USD).](https://pc-zeus.com/bto/bto-gpuserver-Core1700/3430/system_detail.html)

The prompt was as follows:
>You really want to play Run 3, but your poor Pentium 4 isn't fast enough! You've heard there's a computer shop worthy of thunderous praise in this building, but you need an expert opinion on their services first. If a computer is good enough to work on games, it should be good enough to play them. It’s been rumored that someone who works on games once purchased a computer from here. Can you find their first game?
>
>Flag format: `UMASS{name of the game in English}`, for example `UMASS{Elden Ring}`

I made sure to provide a few hints within the prompt to let people both where to look and that they were on the right track. The key word here is "thunderous", a nod to the Greek thunder god.

Given the image:

![Photo of building in Tokyo, Japan](/images/umassctf-2025/image.jpeg)

The intended solve was that you get the address (東京都台東区北上野2-3-9 北上野ビル2F or Japan, 〒110-0014 Tokyo, Taito City, Kitaueno, 2 Chome−3−9 北上野ビル 2F) from the just barely readable URL of rad-japan.co.jp. They have the building address listed at the bottom of their website, so this is the easiest way. I did run into a few people who did route two: read the street sign (in Japanese) and find the exact location based on that information.

Once you have the address, you can throw it into Google Maps and click on the building (not the RAD listing) which lists all the business that have listings in it.

![Results of the address search](/images/umassctf-2025/results.png)

The correct option is the second. While the first, ACharge, can lead you over to Zeus, the link on their website listed in very small text that is entirely in Japanese, difficult to catch for most people. The second is a landing page for Wistech, the company that owns the Zeus brand alongside a few others (ACharge, VSpec, Hercules). Each of these brands creates computers targeting different markets, with Zeus targeting corporations and individuals looking for high-performance workstations. Once on the Zeus website, there are two places to find testimonials, the [voice section](https://pc-zeus.com/voice/) and the [examples section](https://pc-zeus.com/example.html) (which is also fully listed out on the front page). The latter is where you want to go. The [second PC listed on that page](https://pc-zeus.com/example_13.html) was built for video game music composer Shohei Tsuchiya, who is the person we are looking for. 

![Shohei Tsuchiya's interview page](/images/umassctf-2025/shohei.png)

Searching him up leads us to his [vgmdbf page](https://www.vgmpf.com/Wiki/index.php?title=Shohei_Tsuchiya), where we find that his first work is in *Otogi 2: Immortal Warriors*, a 2003 game by FromSoftware. It turned out to be a complete coincidence that the example game for the flag format was by the same developer, Elden Ring was just the first game that crossed my mind!

This challenge gave people a lot of difficulty. In my head, I was worried that it was going to be too easy! Play-testing it led me down a clear path, but it was only until people started their own solves when I realized that the actual solve was a bit more convoluted. Firstly, Tsuchiya isn't the only person who works on games that Zeus has built computers for. Many people found other game developers like [this guy who needed a PC for creating pre-rendered cutscenes](https://pc-zeus.com/voice01.html) (he even used a Pentium 4 back in the day!). Secondly, my language in the prompt was originally a bit unclear to some, as I used the term "game developer" instead of the current "works on video games" which seemed to lead more people to the composer. Lots of people also got lost in the Wistech maze as ACharge shows up first on the Google Maps results, and the layouts on all the websites are such a mess that it can be hard to tell what you're even looking at. I think a lot of people also got caught up in looking for explicit mentions of games when you had to click through to the interview with Tsuchiya to see any mention. Overall, I'm really happy with how this challenge turned out, and I'm really happy to see that people liked it and found it unique.

Shout out to Suvoni in the Discord server:

![They actually visited the building!](/images/umassctf-2025/legend.png)

## Multiplayer
Since people were struggling to solve *Attack*, I wanted to throw in an easier challenge to give the beginners something to work off of. I scrambled to throw together a challenge based on an idea I had leading up to the CTF, and well, it was certainly easier. I took special care to make sure that both of the street names in the intersection were visible and that the premise was clearer than *Attack*.

>You and a friend want to play Fireboy and Watergirl in the Forest Temple, but you both live quite far away. You both want to meet up roughly halfway by distance, you want to meet at a place that has public computers, and you want to meet up at a place that shares the name of the street where you both live. What’s the address of where that could be?
>
>Flag format: `UMASS{Address as on Google Maps}`, e.g. `UMASS{650 N Pleasant St, Amherst, MA 01003}` for the Integrative Learning Center at UMass.

Our two images respectively:

![Location 1](/images/umassctf-2025/multiplayer1.jpeg)
![Location 2](/images/umassctf-2025/multiplayer2.jpeg)

Finding the locations isn't too difficult. You can brute force it by just Googling the intersection, or taking a more meticulous approach and searching by municipality or via a street number from one of the visible houses.

[Location 1](https://www.google.com/maps/@37.6496951,-77.4639334,3a,85.9y,354.91h,82.64t/data=!3m7!1e1!3m5!1slmKLvrETVqPuVByjzdpsBw!2e0!6shttps:%2F%2Fstreetviewpixels-pa.googleapis.com%2Fv1%2Fthumbnail%3Fcb_client%3Dmaps_sv.tactile%26w%3D900%26h%3D600%26pitch%3D7.362741701533622%26panoid%3DlmKLvrETVqPuVByjzdpsBw%26yaw%3D354.9063755287497!7i16384!8i8192?entry=ttu&g_ep=EgoyMDI1MDQxNi4xIKXMDSoASAFQAw%3D%3D) and [Location 2](https://www.google.com/maps/@40.6130276,-75.5048425,3a,89y,83.68h,87.7t/data=!3m7!1e1!3m5!1sUlfcq5EKgG2V9LRTbLxfnQ!2e0!6shttps:%2F%2Fstreetviewpixels-pa.googleapis.com%2Fv1%2Fthumbnail%3Fcb_client%3Dmaps_sv.tactile%26w%3D900%26h%3D600%26pitch%3D2.3032104072804884%26panoid%3DUlfcq5EKgG2V9LRTbLxfnQ%26yaw%3D83.67616530918039!7i16384!8i8192?entry=ttu&g_ep=EgoyMDI1MDQxNi4xIKXMDSoASAFQAw%3D%3D)

From there, all you need to do is take the addresses from the locations and plug them into a website like [whatshalfway.com](https://www.whatshalfway.com/search.aspx?search_type=WHW&addr1=1199%20N%2019th%20St%20Allentown,%20Pennsylvania|&addr2=1398%20Pennsylvania%20Ave%20Glen%20Allen,%20Virginia|&stop1=&avoid_tolls=False&avoid_highways=False&travel_mode=driving) (or just eyeball it) to find the relative midpoint by distance, which is smack dab in the middle of the Fort McHenry Tunnel in Baltimore. From there, it's an easy Google search with the Pennsylvania and library clues to lead you to the "Enoch Pratt Free Library - Pennsylvania Avenue Branch," with its address being 1531 W North Ave, Baltimore, MD 21217.

In my haste to get the challenge out quickly, I forgot to strip the EXIF data from the images, which I noticed once someone asked me for hints for what to do after obtaining the panorama IDs from the images. Rookie mistake on my part, but for the people who solved it in the first twelve hours or so had the opportunity to take an easy challenge and make it trivial. I heard someone even got a solve with ChatGPT, which is definitely something. Not much else to say about this one, I think the concept can definitely be expanded upon and made a bit more difficult.

All in all, it was a ton of fun writing these challenges and responding to your (many) tickets. I learned a lot and plan to make some even more devious challenges next year. Until next time!