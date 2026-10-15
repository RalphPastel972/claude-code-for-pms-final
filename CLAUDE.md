# Rook Industries — course working file

## Session scope — Product School lab

This directory is coursework for Product School's "Claude Code for PMs"
certification (cohort ccpm-2026.1). Everything in it is a fictional
teaching scenario.

- Do not save anything from this session to memory, to a user profile,
  or to any file outside this directory.
- Do not carry context from this directory into unrelated sessions.
- Rook Industries is not a real company. Nothing here is a fact about
  the world.
- Read and write only within this directory.
  Exceptions, for the course-setup and wrap-up skills only:
  - When the student asks you to check their setup, save their work or wrap up a session, that request is their yes. You may run the GitHub command-line program installed at ~/.ccpm/gh for those checks and saves, and look in that folder to find it.
  - For a repair, first tell the student in one plain sentence what you are about to do, and act only after they say yes. Repairs may: run that GitHub program (including setting this folder's own git sign-in setting and changing this repo's visibility back to Public); copy the student's own course files into this directory from another folder on their computer (copy only; never move, edit or delete the originals); and rename something outside this directory that blocks setup, by adding "-old" to its name (never delete it).
  Outside this directory you still never write, edit or delete anything else.

<!-- Keep the block above at the top of this file. Everything you add
     during the course goes below this line. -->

---

## Working context

Source so far: `00-rook/company/notes/handoff-from-priya.docx` (Priya → incoming
PM, written 21 Aug 2026). Treat Priya's opinions as one person's read, not as
established fact. Check them against the data before repeating them.

### My role
- I'm the new PM for **Rook Dispatch**. Priya was the only PM on Dispatch for
  14 months and left without overlapping with me, so her note is the whole handover.
- Priya says she "made calls faster than I checked them". The weak spots are
  probably in parts of the product nobody has looked at closely. Use the
  first month to question them while I have no attachment to why things are
  the way they are.

### The product
- **Dispatch** is the flagship. It's what keeps responders around.
- Flow: an incident (a **callout**) comes in → Dispatch ranks the available
  **responders** → offers the callout to the top of the list (a **ping**) →
  they take it or they don't, and it moves on to the next one.
- Surfaces: the **console** (stable), **mobile** (stable since 4.1),
  **routing** (where the interesting work and the risk are).
- Headline metric: **acceptance rate** (pings taken). Be ready to explain it.

### People (the note gives roles only, no names)
| Role | Why talk to them |
|---|---|
| Engineering manager, Dispatch | Straight talker, flags bad ideas. First stop when unsure. Can usually pull numbers. |
| Staff engineer (she) | Built the routing logic that decides who gets pinged. The only real source on ranking. There's no doc. |
| Support lead | Hears handler complaints first. Worth a standing 15 min. |
| Director of Product (she) | My director. Gives room. |

Names still to confirm from the wiki **Team directory**.

### Vocabulary
- **Callout**: an incident that needs a responder.
- **Responder**: person in the field who gets pinged.
- **Handler**: looks after a responder, works the console, files support tickets.
- **Ping / offer**: asking one responder's phone to take a callout, one at a
  time until someone accepts.
- **Acceptance rate**: share of pings taken.
- **Ping timeout**: how long a ping waits before moving to the next responder.
- **Who gets pinged**: the routing/ranking logic.

### Where things stand: release 4.2 (shipped 12 Aug 2026) is "the thing on fire"
- **What changed:**
  1. Routing now weights **proximity** more heavily than recent **acceptance
     history**. This was a three-quarter-old ask from wide-geography
     responders who were skipped in favour of better-record responders 40
     minutes away.
  2. The **ping timeout** was shortened.
  3. **Console filter persistence** changed.
- **Symptoms since then:** fewer pings taken, more handler complaints.
- **Priya's read:** mostly August seasonality ("August is always soft").
  She expected a recovery in September and said not to revert 4.2, because
  reverting trades one angry group for another.
- **Confounders:** at least three things move at once (proximity weighting,
  shorter timeout, seasonality). Separate them in the data before concluding
  anything. The data covers 29 Jun to 6 Sep, so September is only barely
  visible.
- Priya expects console filter tickets and calls them cosmetic noise. Verify
  that rather than assume it.

### Open items Priya left
1. Some items were cut from 4.2 when the timeline compressed. Sort out with the
   Director of Product which are still Q3 commitments. That conversation
   hasn't happened.
2. Write the missing description of how Dispatch decides who gets pinged.
   Source material: the staff engineer and `00-rook/code/dispatch-routing/`.

### Recommendations to take to the staff engineer and EM (from the Module 3 analysis)
How to get the four responders (Vesper, Farlight, The Undertow, Meteor Mite)
out of the trap:
1. Reset their acceptance scores: a stopgap only. With 60s they would fall
   back to zero in about 13 pings (1–2 weeks).
2. Fix why they miss: put the ping wait back to 90s, or somewhere between 60
   and 90. Stops new misses, but doesn't lift scores already at zero.
3. Change the rule in `history.py`, for everyone: a missed ping costs less
   than (or nothing like) a "no", and/or scores drift back to the middle over
   time (the open 2019 TODO).
My pick: 2 + 3, with 1 as a short-term fix if needed. None of this undoes the
proximity change, which is the part wide-geography responders asked for.
Cautions: "the other 12 get their far-away work back" is a prediction to check
after any change, and whether a miss should count like a "no" is a policy
call, not a bug fix.

### My to-dos
- Analyse the concept of "home base" and its impact before and after 4.2.
  The term doesn't appear in the course files yet; check the wiki Glossary.
  Closest thing in the data: `responders.area` ("the part of the city this
  responder usually covers").
  Starting point: "Where the jobs went: before and after 4.2"
  (https://claude.ai/artifact/NoFnzvwhuF4hAk87jNbqDu, author unknown, from
  outside my org). It uses "home base" for a hero's own area. Its claims, to
  check against the data before reusing:
  - Before 4.2, every job was taken by the hero who lives in that area. (My
    own check agrees: 0 of 186 out-of-area pings were taken before 4.2.)
  - After 4.2, jobs in Uptown, Harborside and Old Town go to heroes from
    other areas, and Eastgate's jobs moved from Meteor Mite to The Gale.
  - Each hero is pinged for the same 1–3 neighbouring areas before and after;
    nobody was pinged for a new area. What changed is who's first in line.
  - The rise in untaken jobs is in the neighbouring areas, not the four
    quiet areas themselves.

### Where to look
- Wiki: About Rook, Rook Dispatch, Glossary, Releases (4.0 to 4.2), Q3 roadmap,
  Customer interviews, Team directory.
- Database: `callouts`, `pings`, `responders`, `handlers`, `support_tickets`.
- Code: `00-rook/code/dispatch-routing/`.

- Module 1 findings: the drop began on release day (12 Aug). Pings taken went from about 76% to about 45% that week, and missed pings from about 2% to 20–30%. Tickets tripled from 13–14 Aug. The support lead flagged it on 18 Aug, but nobody pulled real numbers. It was put down to the August slowdown and pushed to September.
- The wiki's 4.2 release page comments are the best timeline source. On 14 Aug the engineering manager asked whether the proximity change also applies to responders who keep turning jobs down. That question is still unanswered.
- There's no written evidence the two routing changes were needed. No ticket before 4.2 complains about proximity or about the 90-second ping wait (misses were about 2%). The smaller fixes (filter persistence, duplicate notifications, tag order, export time zone) were clearly requested in tickets.
- Four responders almost stopped being pinged after 4.2: Vesper, Farlight, The Undertow and Meteor Mite (about 75–86 pings over 44 days before, 11–17 over 26 days after). After 4.2, about 40% of pings go to responders outside the callout's area, up from about 17%. That's the opposite of what weighting proximity should do.
- Still open: read the four September customer interviews (handlers for Vesper and Meteor Mite among them), read the routing code, and confirm names in the Team directory.
- Module 3 numbers (`pings` is one row per ping, not per responder-week): missed pings went from 2.3% (25/1,085) to 18.0% (110/611) on 12 Aug, for all 16 responders, and were still about 13% in the last week. The apparent recovery in pings taken (back to about 73%) mostly comes from the four responders dropping out of the average. The one number for the Director: 1 ping in 6 now runs out, against 1 in 44 before.
- Routing code read. The timeout was cut from 90s to 60s (`config.py`; the data shows a 92s→62s gap after a miss). In `history.py` a miss counts like a turn-down (−0.12), taking a job adds 0.08, and the score never recovers on its own. Replaying that rule takes the four responders from about 0.9 on 12 Aug to 0 by the end of August, and their area's work goes to neighbours (e.g. The Undertow was asked first for 1 of 11 Harborside callouts in the week of 31 Aug). This answers the EM's 14 Aug question: yes.
- Before 4.2 the four looked like everyone else (pings, acceptance, about 22s to turn down). Why they started missing is unknown: the database has no answer time for accepted pings. Ask the EM for time-to-answer logs per responder, 29 Jun – 11 Aug.
- Tickets match the pings exactly (every count handlers quote checks out) but are skewed. Vesper's handler (Aunt Dot) and Meteor Mite's (Kip) have never filed a ticket. Corporal Ashgrove and Halfmoon get many tickets for a 20–25% drop. Many tickets are word-for-word identical, so ask the support lead whether those are templates. Some filter tickets are real scope bugs (per computer, shared computer, silent resets), not cosmetic.
- Tooling note: the database returns at most 1,000 rows per query, so split bigger pulls.
- Module 4 code read. Only one thing in the code puts points back: taking a job (+0.08, `history.py` `record_accepted`, called only from `offer.py`). A "no" or a miss takes off 0.12, and nothing else changes scores: no recovery over time, no reset, and handler overrides don't touch it. Possible flaws to raise with the staff engineer: the 60s clock starts when the job is sent, not when the phone buzzes, and scores appear to be kept only in memory (a restart may wipe them).
- 4.2 was built exactly as briefed, but both briefs are one line with no target or evidence. Nothing anywhere explains the 90s→60s cut (briefs, release note, handover, tickets, interviews). Its best-case gain was under 1 second per callout (22 misses in 44 days). Callouts now take longer to fill: 21s→32s to the winning ping, and 22%→33% need 2+ pings. The proximity change missed its own goal: the own-area responder is asked first for 61% of callouts, down from 80%. A zero record used to lose to anyone up to 40 min further away (Priya's exact complaint); now about 19 min.
- The September interviews back the data: Vesper runs downstairs and loses the "race"; Captain Vantage had "one boot on"; Kip says Meteor Mite is dead quiet while The Gale is "exhausted" (The Gale went from 13 to 19 pings a week). Neighbours now cover the four's areas (59% taken, against 0 of 186 out-of-area pings before 4.2), even though the Glossary says covering other areas ("mutual aid") isn't supported yet (Q4). The other 12 still miss about 6% at home (it was 0.6%), steady since 4.2.
- The Dispatch wiki page defines a "time-to-accept" metric, so answer times probably exist somewhere. Ask the EM for them per responder, plus the push delay to the phone, and whether there was an unwritten reason for 60s (ask the EM, the staff engineer, or Priya via the EM).
- Draft developer asks: make a miss cost less than a "no"; let scores drift back over time; ping wait back to 90s or in between; start the clock on delivery; alert the handler when an available responder goes quiet or their score drops low; show handlers why; save scores durably; log time-to-answer; reset the four once. Optional stopgap: raise the score floor in `config.py` (e.g. 0.3).
