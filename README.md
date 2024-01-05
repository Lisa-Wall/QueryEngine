# QueryEngine
HotSite bug fix and dll patch

This is the achievment I'm most proud of while working at Cognos. 

There was a bug somewhere deep in the bowles of the query engine. The query engine was a collection of functions written in C++ which took in SQL queries and transformed them into their final forms. Somewhere along the way, certain types of requests were producing mal-formed queries, which of course returned incorrect data from the database. This was a pressing issue because some clients were reluctant to upgrade the software, yet they were experiencing this issue. They needed a targeted fix involving just a few dlls.

Finally, I decided enough was enough, and I came in on a weekend, 2 days straight for a total of 21 hours, until I FIXED THE BUG!!!!! I remember the exhileration of it, the sheer extacy when I found the problem. Of course there was no one else in the office, so the moment I figured it out I remember jumping up and yelling and dancing among the cubicles. Ah, what a wonderful time!

Once I found the bug, the fix was easy, and I went on to write a 22 page document about it.

This document went up the management ranks, and I was eventually called to meet one of the bigwig managers. He asked me if I could write a program to detect if clients would be affected by this bug. I wrote the program, a simple script, which would print a text file that gave you a flag. It would print red flag if you had the bug, a yellow flag if you were in danger of having the bug if you changed anything in the query, or a green flag if you were ok. This got posted on a website somewhere where clients could download it and "self-diagnose" themselves. If they had the bug they could also download the patch, which was a set of dlls I produced which contained the bug fix. They could drop these into their existing install, instead of upgrading their whole software version. That was the whole thing about it - these clients were on old versions of the product and reluctant to upgrade.

------------ TECHNICAL ---------------

The crux of the bug was that a "group by" clause was failing to be produced, which led to a cartesian product being performed on two tables, hence the extra rows. The query engine was cutting off too early, where it should have continued on to perform several more transformations before arriving at the final sql. The result was that the query sent to the database was incomplete, and returned far too many result rows. 

I remember once I "got it", I could come up with queries in other similar forms that I knew would fail. I would be able to tell by looking at a client's query, whether they would have a problem. I realized it was possible for the query to become so mangled as to crash the program. This was a critical problem, and this is why management decided they needed to open a "HOTSITE" for it, and produce a patch and diagnostic tool for clients. I was proud to have been in charge of a hotsite.

Here is the original, incorrect series of queries as they passed through the query engine. They should be equivalent, yet they are not. The "for" clauses in the second query should be consolidated into a "group by" clause in the 3rd query, but it is missing.

![Original Code](https://github.com/Lisa-Wall/QueryEngine/assets/155689251/54fed9f3-15b0-4319-95b7-7a1409df5a17)

Once the query engine was fixed, the proper "group by" clause was produced, and the query went on to pass through several more transformations, arriving at its correct final form.

![Final Code 001](https://github.com/Lisa-Wall/QueryEngine/assets/155689251/8cf8c200-b677-440a-b35a-345e0f173465)
![Final Code 002](https://github.com/Lisa-Wall/QueryEngine/assets/155689251/90267ffc-df00-4ab4-ab37-b411c69db4aa)




