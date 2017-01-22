---
layout: post
title: Export highlights and notes from personal side-loaded Kindle Documents
date: '2017-01-23 08:55'
categories: howto
---

When I finished reading [Cal Newport](http://calnewport.com/)'s [Deep Work](http://calnewport.com/books/deep-work/), I wanted a way to export my side-loaded Kindle highlights into a text format for simple access, so that I can further annotate them and publish a review.

Highlights / notes are saved into a "My Clippings.txt" file in the "documentS" folder of the kindle, accessible when it's mounted in USB drive mode. But this data is unsorted, and each entry has all sort of metadata which clutter up the notes.

Google led me to [Jane Dallaway[(http://jane.dallaway.com/)'s [Kindle Helper Scripts(https://github.com/janedallaway/Kindle-Helper-Scripts), which turned this ugly mess:

  ==========
  Deep Work (Cal Newport)
  - Your Highlight at location 464-466 | Added on Saturday, 14 January 2017 09:13:02

  The results from this and her similar experiments were clear: “People experiencing attention residue after switching tasks are likely to demonstrate poor performance on that next task,” and the more intense the residue, the worse the performance.
  ==========
  Deep Work (Cal Newport)
  - Your Highlight at location 475-477 | Added on Saturday, 14 January 2017 09:14:37

  That quick check introduces a new target for your attention. Even worse, by seeing messages that you cannot deal with at the moment (which is almost always the case), you’ll be forced to turn back to the primary task with a secondary task left unfinished. The attention residue left by such unresolved switches dampens your performance.

Into this nice clean text format:

  Deep Work by Cal Newport

  The results from this and her similar experiments were clear: “People experiencing attention residue after switching tasks are likely to demonstrate poor performance on that next task,” and the more intense the residue, the worse the performance. (464)

  That quick check introduces a new target for your attention. Even worse, by seeing messages that you cannot deal with at the moment (which is almost always the case), you’ll be forced to turn back to the primary task with a secondary task left unfinished. The attention residue left by such unresolved switches dampens your performance. (475)
