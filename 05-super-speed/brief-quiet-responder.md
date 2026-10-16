# Brief: A way back for a responder who has gone quiet

**For:** Helen Achebe, Director of Product | **From:** PM, Rook Dispatch | **16 Oct 2026** | **Draft**
Data covers 29 Jun to 7 Sep 2026 only. Today's state is unknown.

## Summary
Release 4.2 (12 Aug) cut the ping wait from 90 to 60 seconds. A missed ping now costs the same as a turned-down one, and a lowered score never recovers by itself. Four responders, including The Undertow, went from about 12 pings a week to 1 and have not come back. We would build a visible way back, not a quiet number change.

## Who it is for
**The Undertow**, a responder in Harborside, and their handler **Desmond Okafor**. Handlers like Kip are the same kind of user.
- Before 12 Aug: about 12 pings a week, about 9 taken.
- 12 to 16 Aug: 5 of 8 pings missed. Last taken ping 17 Aug. Then 1 ping a week.
- Okafor has 11 open ping tickets. He says availability is set correctly and the ping is "gone before he could answer."

## What changes for them
**Okafor opens the console and sees:**
- "The Undertow has gone quiet." 1 ping this week, was about 12.
- Last 8 pings: misses and turn-downs shown separately.
- Two actions: **Give a fresh start**, or **Mark this miss as legitimate**.

**The Undertow notices:**
- A ping again after weeks of silence.
- A missed ping no longer counts like saying no.
- In the phone app (proposed, not yet designed): a plain line saying why pings dropped and that the handler can restart them.

**Nadia Hoffmann (Support):** fewer "my phone never goes off" tickets, about two-thirds of her 26 Aug split.

## Proposed solution
The wait stays at 60 seconds. Restoring 90 stays an option, decided on Ravi Menon's response-time data, never quietly. Order of work:
1. **Check unfilled callouts first** (Marcus Oyelaran). If any went unfilled, this comes before everything else.
2. **Cheaper miss, plus a fresh start, together** (S and S-M, both guesses). Neither alone works. A fresh start with no change to the miss cost sends The Undertow back to the floor in about 4 misses. Pilot with The Undertow only.
3. **Gone-quiet alert** in the console (M, guess). Ravi sets what counts as quiet.
4. **Handler marks a miss legitimate** (M, guess). Second step. It adds handler work, and the console may not show misses today.
5. **Logging** (S to M, guess): weekly pings per responder against their own baseline, real scores at ranking, and who was next when a miss ended a callout.

**Deliberately not included:**
- No quiet revert of the wait or the proximity weights.
- No per-responder wait. It is one global setting.
- No link between cover identities and legal identities (Security Policy 4.1).
- No "tap to hold" button. It could answer "gone before I could answer," but it is large and unknown. Worth exploring with Sofia Marino.
- No promise of a fix before Wen Li replays the real scores.

## Why it happens (three layers)
1. **Trigger, confirmed as timing:** the wait went from 90 to 60 seconds. The gap after a miss went from 91-93s to 61-63s, and misses rose for all 16 responders. The weights changed in the same release.
2. **Trap, likely:** a miss costs 0.12 and a taken ping adds 0.08. No decay (2019 comment in `history.py`, never answered). Someone who falls behind gets few pings and cannot climb back.
3. **Blind spot, least understood:** 49 of 440 callouts since 12 Aug had no taker (48 of 879 before). 23 ended on a missed ping, 21 of those with one ping. A miss on a short list may end the callout with no retry. This is a guess, and only 6 of the 23 involve the four. It may hurt customers.

## Confirmed, likely, unknown
**Confirmed:**
- Missed pings: 2.3% before 12 Aug (25 of 1,085), 18.0% after (110 of 611).
- The four went from about 49 pings a week combined to about 3.
- Miss counts as decline. Nothing but a taken ping raises a score.

**Likely:**
- The score loop kept the four quiet. My rebuilt scores put them at 0 by 27 Aug to 5 Sep. They were high going in, so the loop explains staying quiet, not starting.

**Unknown:**
- Why the four missed their first pings. Decline habit, area, time of day and busy-ness are ruled out. Clue from Aunt Dot: the phone buzzes and the ping is gone before they reach it.
- Whether any no-taker callout went unfilled, and what happens when the candidate list ends.
- Whether proximity was meant to apply to decliners. Marcus asked on 14 Aug and nobody answered.
- What score a fresh start sets (0.5 is my guess) and who may request one.
- Whether the console shows handlers per-ping history, and where scores are stored.

**What would change my mind:** if the replay shows the four's rank did not fall (this needs travel times and availability, not only scores), the score-loop idea is wrong.

## Timeline (all dates proposed)
| Step | Owner | When |
| --- | --- | --- |
| Unfilled callouts, real scores, storage | Marcus Oyelaran, Wen Li | 23 Oct |
| Response times, quiet threshold | Ravi Menon | 23 Oct |
| Handler calls (Okafor, Pruitt, Kip, Aunt Dot) | Me | 23 Oct |
| Console and phone-app design | Sofia Marino | 30 Oct |
| Helen picks the options | Helen Achebe | 6 Nov |
| Build and release | Marcus's team | Next monthly release after sign-off. Date unknown. |

## Who I need to ask
- **Marcus:** unfilled callouts, deploys since 12 Aug, who is next when a home responder misses.
- **Wen Li:** real scores, travel times, push times, intent behind the 2019 comment.
- **Ravi:** time from ping sent to taken, and a rule for "quiet."
- **Sofia:** console and phone-app design.
- **Okafor, Kip, Aunt Dot, Pruitt:** phone model, location, settings, anything that changed on 12 Aug.

## Success looks like
- The Undertow is pinged at about its old rate (about 12 a week). Proposed.
- Misses fall toward the pre-4.2 level (about 2%).
- No rise in no-taker callouts.
- Okafor's open ping tickets close.
