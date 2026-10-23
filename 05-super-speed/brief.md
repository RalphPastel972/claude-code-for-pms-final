# No responder goes quiet without anyone knowing

**Draft for Helen Achebe · Rook Dispatch · October 2026** ·
**Click-through:** [Gone Quiet Prototype](https://claude.ai/artifact/9gmqGBSYEVz5NWbbkQW9qd) (Kip's card and Meteor Mite's phone; file: prototype.html)

## The problem

Kip looks after Meteor Mite and The Gale, who both cover Eastgate. Since 4.2
(12 August), Mite's phone has almost stopped ringing and The Gale's never stops.
Kip says Mite "thinks Mite's been forgotten" and The Gale is "exhausted". Nothing
in the console told him why, and he has never filed a ticket, so tickets missed it.

| | Before 4.2 | Since 4.2 |
|---|---|---|
| Meteor Mite: pings a week | about 11 | **1–2** by late August |
| Meteor Mite: pings missed | 3% | **57%** |
| The Gale: pings a week | about 13 | **about 21** by late August |
| All responders: pings missed | 2.3% (1 in 44) | **18%** (1 in 6); 13% latest week |
| Time to answer a ping | 90 seconds | **60 seconds** |

Four responders went quiet this way, but everyone is hit: the other 12 miss about
6% of pings in their own area, up from 0.6%. Data runs to 6 September.

## Why it happens (likely, not proven)

1. **The time to answer was cut to 60 seconds**, with no written reason. Vesper's handler
   describes him losing the race down the stairs to his phone. (No answer-time data exists yet.)
2. **Running out of time counts as a "no"**, which pushes the responder down the queue.
3. **The only way back up is taking a job**, and people at the back are rarely asked.
   Wen Li raised this in 2019; it was never decided.

## What we'd build

- **Kip sees a "gone quiet" warning** with the reason in plain words. *Example only:*
  "Available but not asked in 5 days. 5 of the last 6 pings ran out of time."
- **Kip can put the responder back in the queue** (*new*: today nothing a handler does
  changes their place). It restores their place once, and records that Kip did it.
- **The phone says "This one moved on. You're still on the list."** It ships only with
  the rule changes below, or it wouldn't be true.

We are **not** reverting the proximity change, which wide-area responders asked for.

## Decisions for Helen (these affect all 16 responders)

| Decision | Trade-off | PM leans |
|---|---|---|
| Reset the four now | Pinged again this week, but at 60s it lasts only ~13 pings | Yes, as a stopgap |
| Wait time: 90s or in between | Fewer misses vs. slower hand-off after a miss | Back toward 90s |
| Cost of running out of time | Free would tempt people to let pings run out instead of saying no | Less than a "no" |
| Recovery over time | Today places never recover on their own | Slow drift back |
| Warn the handler after X quiet days | Too soon is noise, too late is silence | Set with Kip and Sofia |

## Success (proposed)

Missed pings back near 2%; jobs filled in about 21 seconds again (32 now); no
available responder quiet for X days without their handler told. Ravi Menon tracks it weekly.

## Still to confirm

- **Facts:** answer times (Ravi or Marcus); how long a ping takes to reach the phone
  (Marcus); where queue places are stored, and whether a restart wipes them (Wen);
  any unwritten reason for 60s (Marcus).
- **Voices:** Meteor Mite directly, via Kip and Sofia Marino. This brief rests on Kip's
  account. Rook Supply, if availability recording changes.

*Sources: Rook database (pings, tickets), routing code, wiki, September interviews.*
