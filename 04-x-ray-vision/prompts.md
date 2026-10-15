# 04 · X-Ray Vision — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. Last session the numbers showed you what happened: a
ping used to wait ninety seconds and now it waits sixty, people
missed pings they used to catch, and missing one counts the same as
turning one down — so four responders stopped hearing from us
altogether.

At the end of the session, type wrap up, and Claude Code saves the
prompts you wrote yourself below — not the starter prompt — updates
CLAUDE.md, and saves your work to GitHub. By Module 6 this file is a
prompt library built from your own questions.

---

### 1.
Is that possible that because of the many "don't answer in time" of some responders, their records went too low and therefore their phone didn't ring, so the calls went to other responders who typically do not reply on time, all that causing a negative feedback loop ?

### 2.
"The release caught four responders in a trap they can’t get out of. Their neighbours were stretched for a couple of weeks but recovered. There’s no sign of the trap spreading to everyone." Ok, understood.
But you said they managed to get their score back up right? So do I assume correctly there is another issue that explains why they still do miss so much of the pings?

### 3.
"Freeing the four would also give the other 12 their far-away work back." what do you mean by freeing the four ? Do you mean increasing their score ?

### 4.
those recomendations are awesome. remember them for later.

Now, tell me if the code actually does a reduction of the wait time from 90s to 60s ?

### 5.
use all the data sources plus this code walkthrough to help paint a picture for me on what is going on. i want to understand if what was asked to be build was actually built as intended, whether there's any bugs, and what would i tell a developer to do if we decided we want to make any change to prevent heros from silently existing the system because they missed/ignored/rejected a call

### 6.
Find me the part of this code that takes points off somebody when they miss a ping or turn one down. Show it to me and explain it in plain English. Then find me every single thing in this code that puts points back on.

### 7.
Regarding "recovering context", I got a waaay stronger result using those two promts:

1. Look at all the topics we discussed so far, give me a promt that provides an interactive story artifact in html of the entire problem like a cartoony teaching story for class members. The story needs to follow a classical Product structure: success metrics, insights/observation, problem, ranked possible solution. Go deep in linking data and artifacts so you did a due diligence before reporting an anyone can recheck the claims.


1. I realised, most of my past promts where not there. so Context and then please catch up: I am new PM and need to see if any fires have to be put out for the past release that I missed, So you need a deep critical view into The tickets, into the pings, into the interviews and then compile a challenged roundup on the current situation (you can look at past prompts on the wrapped up files) Finally: <Paste the result of 1. >

### 8.
Do we know what was the reasoning when we decided to go from 90 sec to 60 sec ?
