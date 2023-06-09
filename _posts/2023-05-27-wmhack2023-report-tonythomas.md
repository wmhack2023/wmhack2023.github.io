---
title: Report on Wikimedia Hackathon 2023, Athens
author: tonythomas01
date: 2023-05-27 17:30:00 +0200
categories: [Blogging, Sessions]
tags: [wmhack2023volunteers, reprot, day1, day2, day3]
image:
  path: https://upload.wikimedia.org/wikipedia/commons/e/ed/At_Wikimedia_Hackathon_Athens_%28MP%29_2023_001_%28cropped%29.jpg
  alt: Wikimedia Hackathon 2023
  style: background-color:white;
---

The 2023 edition of Wikimedia Hackathon has just concluded, and I was one among the lucky participants to join on-site.
It was a great feeling to re-connect with fellow Wikimedians after 4 long years of no-onsite events, and to be part of a
community that thrives for free knowledge and code.

**tl;dr**: We built a user-script to summarise article sections on wiki pages. Check
the [code](https://github.com/tonythomas01/wikipedia-section-summaries)
and [demo](https://www.youtube.com/watch?v=mja1C6FnWes).

![Project Demo](https://upload.wikimedia.org/wikipedia/commons/d/dd/Wikipedia_section_summarizer_demo.gif)

## Pre-hackathon statelite event in Stockholm

We had the idea of organizing a satellite event in Stockholm, and thanks
to [the support of WMSE (Wikimedia Sweden)](https://se.wikimedia.org/wiki/St%C3%B6d_till_gemenskapen/Projektst%C3%B6d/Pre_Wikimedia_Hackathon_Stockholm_2023)
at the opportune moment, we were able to secure the necessary space and time to host it.
I would like to express my gratitude to [Axel Petterson](https://www.mediawiki.org/wiki/User:Axel_Pettersson_(WMSE)) for
assisting in the setup process. During this time, we also had a productive brainstorming session to determine the
activities for the main hackathon.

Personally, I was eager to reconnect with the community after a period of relative inactivity,
so it was important for me to gauge their interests. [Lokal_Profil](https://phabricator.wikimedia.org/p/Lokal_Profil/)
and [Sebastian_Berlin](https://phabricator.wikimedia.org/p/Sebastian_Berlin-WMSE/) graciously attended the event,
and together we explored potential ideas for hacking during the main hackathon. Their expertise and insights into
[Wikispeech](https://meta.wikimedia.org/wiki/Wikispeech) (text-to-speech functionality on wiki pages) sparked
discussions related to improving accessibility and readability.
Many interesting project ideas were pitched and hacking has already started for a lot of them. In person socialising,
after several years, allowed spontaneous interaction to emerge and collaborations are already on the way.

| ![Image 1](https://upload.wikimedia.org/wikipedia/commons/1/1c/Stockholm_pre_hack%2C_2023-05-15%2C_08.jpg) | ![Image 2](https://upload.wikimedia.org/wikipedia/commons/6/69/Stockholm_pre_hack%2C_2023-05-15%2C_02.jpg) |
|:----------------------------------------------------------------------------------------------------------:|:----------------------------------------------------------------------------------------------------------:|
|                            From Pre Wikimedia Hackathon, Stockholm on 15th May                             |                            From Pre Wikimedia Hackathon, Stockholm on 15th May                             |.

More pictures
here: [Category:Stockholm_pre_Hackathon_2023](https://commons.wikimedia.org/wiki/Category:Stockholm_pre_Hackathon_2023)

Towards the end of the event, with the help of Axel's contributions and great refreshments, we came up with a feasible
hackathon idea. Here are some refined iterations we discussed:

1. Summarising info-boxes on wiki pages: We explored the possibility of
   enabling [Wikispeech](https://meta.wikimedia.org/wiki/Wikispeech) to read out loud the summarised content from
   info-boxes.
2. Summarizing entire article pages: We considered developing a system to generate concise summaries of complete
   articles.
3. Summarizing article sub-sections: We discussed using user-scripts and Wikimedia infrastructure to create summaries of
   specific sections within articles.

During our discussions, we made initial plans to
leverage [ChatGPT chat-completion](https://platform.openai.com/docs/guides/chat) endpoints for
generating sub-section summaries. We also created an architecture diagram to visualize the implementation. To organize
our efforts, we promptly created a Phabricator [task](https://phabricator.wikimedia.org/T336692), and we were fortunate
to have [Tgr](https://phabricator.wikimedia.org/p/Tgr/) join our team. Tgr suggested
expanding the summarization feature to include Talk pages. Additionally, [Tgr](https://phabricator.wikimedia.org/p/Tgr/)
proposed the idea of using cookies or local
storage to securely store OpenAI secrets, aiming to enhance user satisfaction and trust in the system.

## Main hackathon at Technopolis

Athens is a beautiful place, and there is something historic on any corner you look. That was my impression of the city.
We were accommodated and taken care of with a lot of planning and precision, and I thank the organising team for that.
[Technopolis](https://www.mediawiki.org/wiki/Wikimedia_Hackathon_2023/Venue) was a great location as well, and we
started the hackathon on time on the 19th. I was also part of the Trust
and Safety team, and thanks to nothing going sideways, we had a relaxed hackathon.

During the idea pitching phase (strictly controlled to 30 seconds
by [Siebrand](https://phabricator.wikimedia.org/p/siebrand/)), I managed to pitch the idea in-front of
the audience. It was not the clearest pitch, but straight after that, I got 1-2 people interested in the
idea. [Alexey](https://phabricator.wikimedia.org/p/Alexey_Skripnik/)
had a lot of years under his belt in summarising wiki pages (mostly books, if I remember correctly), and then we had a
couple of engineers who where working for the foundation (Wikimedia) along the lines of Machine Learning/ AI.

We found a table, and started working on how it would look like, and thanks to Alexey's frontend/UI expertise, we got a
very nice looking design fast.


> I cannot mention enough the great fresh food, feta-cheese, tomatoes and drinks those were served continuously during
> the hacking days. Thank you.

| ![Our hackathon table](https://upload.wikimedia.org/wikipedia/commons/3/39/Wikimedia_Hackathon_2023_day1_-_06.jpg) |
|:------------------------------------------------------------------------------------------------------------------:|
|                                    Our table, when it was at its busiest state.                                    |

By mid-second day, we got [Tgr](https://phabricator.wikimedia.org/p/Tgr/) too to sit with us, and he wrote a script that
would extract well formatted text data from "Talk" sections on a wiki page. This was crucial, as until that point, we
were relying on scraping text heading by heading to generate the text that has to be summarised.

On the third day, we realised that we have code in 3 repositories which were doing more or less the same thing, but
better.

1. Alexey had the one with the best UI (thanks to his expertise). He had also figured out how to stream ChatGPT
   responses
   right onto the page.
2. [Tgr](https://phabricator.wikimedia.org/p/Tgr/) had the best implementation to read and parse talk section pages (he
   used parsoid-html via API).
3. I had maybe a bit improved version of scraping data under sections. Also, maybe a good way to continuously deliver
   updated scripts (via Github pages).

I got onto the task of merging the best of all these 3 together, and we managed to
get [Github:tonythomas01/wikipedia-section-summaries](https://github.com/tonythomas01/wikipedia-section-summaries/)
before the demo. We created a small 30 second video (linked above), and managed to present it during the showcase. Since
I do not like to see myself talking, I would not point to the time - but its somewhere
in [here](https://www.youtube.com/watch?v=Nd-kckDEaR0) :)

## Future of the tool/script

We gathered a lot of feedback during the hackathon, and I can think about the following:

1. Make the currently used ChatGPT prompt editable for users so that they can ask for further clarifications, or have a
   section explained in a different way.
2. Send the script for evaluation, and maybe make it into a gadget.
3. Explore if we can use any other free LLM models instead. There were a couple of talks about it during the hackathon.
4. Refactoring of the script (in general), and rely on APIs for data, and not text scraping.
5. Open up the script, so that it can be used for
   the [Village Pump](https://en.wikipedia.org/wiki/Wikipedia:Village_pump).
6. Explore how to deliver the script in a better way, and not rely on Github pages.

## Learnings

I would think about the following:

1. Readability and accessibility is an area where generative AI can help Wikipedia a lot. By not necessarily dropping a lot
of quality.
2. From a hackathon point of view: Maybe we should have figured out a way to work together a bit better so that we did not
end up with 3 versions on day 2. This is a challenge when multiple people are working on 1 user script. Hopefully, we
can figure this out soon.

## Other
During my visit, I had the chance to explore the city and even bought a few bottles of delicious olive oil that we've been enjoying. I already miss Athens and hope to return soon. I also had the opportunity to connect with many hackers, students, and staff from the Ionian University. I'm truly grateful to the organizing team for taking care of us during our time here.

| ![Snacks offered during Wikimedia Hackathon 2023](https://upload.wikimedia.org/wikipedia/commons/0/03/Snacks_offered_during_Wikimedia_Hackathon_2023.jpg) | ![Food offered during Wikimedia Hackathon 2023](https://upload.wikimedia.org/wikipedia/commons/2/25/Food_offered_during_Wikimedia_Hackathon_2023.jpg) | ![Rooftop party at Brown Lighthouse hotel, Athens](https://upload.wikimedia.org/wikipedia/commons/b/bd/Rooftop_party_at_Brown_Lighthouse_hotel%2C_Athens.jpg) |
|:---:|:---:|:---:|
| Snacks offered during Wikimedia Hackathon 2023 | Food offered during Wikimedia Hackathon 2023 | Rooftop party at Brown Lighthouse hotel, Athens |
| ![Night view of a street near Technopolis, Athens](https://upload.wikimedia.org/wikipedia/commons/a/a1/Nightview_of_a_street_near_Technopolis%2C_Athens.jpg) | ![Late-night chess after Wikimedia Hackathon 2023 closing dinner](https://upload.wikimedia.org/wikipedia/commons/6/68/Late_night_chess_after_Wikimedia_Hackathon_2023_closing_dinner.jpg) | ![Night view of Omonia street](https://upload.wikimedia.org/wikipedia/commons/3/31/Night_view_of_Omonia_street.jpg) |
| Night view of a street near Technopolis, Athens | Late-night chess after Wikimedia Hackathon 2023 closing dinner | Night view of Omonia street |


Written by [mw:01tonythomas](https://www.mediawiki.org/wiki/User:01tonythomas). Also published in my personal blog [here](https://fosstalks.wordpress.com/2023/05/27/report-wikimedia-hackathon-2023-athens/).
