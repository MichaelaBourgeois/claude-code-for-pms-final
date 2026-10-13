# Module 2 findings: what went wrong with 4.2

Fictional teaching scenario. Written 13 Oct 2026 from the Module 2 session. Data window: 29 Jun to 7 Sep 2026. Each point is labelled as data, document, or guess.

## One-line summary (shareable)

Since 4.2 cut the ping wait from 90s to 60s, missed pings rose from about 2% to 14% and four responders almost stopped receiving pings; the likely cause is scoring that treats a miss as a decline with no recovery (to be confirmed with Wen Li), and we need to check whether any of the 49 callouts with no recorded taker went unfilled.

## What the data shows

- Four responders lost almost all pings after 12 Aug: Farlight, The Undertow, Vesper, Meteor Mite. About 49 pings a week combined, down to about 3. (data: pings table)
- Ten other responders gained 19% to 49% in pings; total pings fell only about 6%. Not an August dip. (data)
- Ashgrove and Halfmoon (quiet tickets, not in the four) fell about a quarter (-27%, -24%) with miss rates of 14 to 15%, in line with the ten, not the 53 to 64% of the four. No one else shows the collapse. (data)
- The four's first pings after 12 Aug: 4 to 5 misses in the first 3 to 5 days, then pings thinned, and almost all later ones were missed. The order of events fits a feedback loop. (data; mechanism is a guess)
- The Gale (same area as Meteor Mite, Eastgate) had 8 misses and still gained pings. Meteor Mite turned down 29% of pings before 4.2 against The Gale's 17%. (data)
- First pings to the home-area responder fell from 80% to 61%. Out-of-area pings missed 30% against 10% in-area, and out-of-area pings rose from 17% to 39% of all pings. (data)
- Pings went to responders from other areas, for example Falkirk, Stormwrack, Nightwell, Vantage. (data)
- 49 of 440 callouts since 12 Aug (11.1%) have no recorded taker, against 48 of 879 (5.5%) before. 23 of the 49 ended on a missed ping. Callouts 41194 and 41228 each had one missed ping and nobody else. Whether any went unfilled is unknown. (data; outcome unknown)

## What the tickets show

- 147 tickets; 40 before 12 Aug and 107 after (about 6 a week to about 29). (data)
- Ping-related: 46 tickets from 12 handlers (16 ping gone, 30 quiet). Only one was before 12 Aug (3014, a lost signal). First post-4.2 ticket 12 Aug; first quiet ticket 17 Aug. (data)
- Four handlers filed 74% of them: Okafor (12), Pruitt (11), Fischer (6), Demir (5).
- All 45 post-12 Aug ping tickets were open at the 7 Sep snapshot. The database has no reply data, so I can't say whether anyone replied. (data; gap)
- All 17 handler ping-count claims and 15 gap claims matched the pings table (counted over 7x24 hours to the filing time). (data)
- Ping tickets explain only about half of the rise in weekly tickets. Filters (14) and other topics also rose. (data)
- Dot (Vesper) and Kip (Meteor Mite) raised it in interviews but filed no tickets.

## What the interviews show

- 3 of 4 handlers described callouts gone before the responder could answer. Dot and Ambrose volunteered it; Halloran said it when asked "anything else?". (document)
- Uneven workload: Kip volunteered it; Dot only said it when the designer asked about quiet weeks (a leading question). (document)
- Ambrose's closest call matches his ticket 3043 (filed 13 Aug): callout 40987 on 12 Aug 19:03, Vantage missed first ping. (data and document)
- Dark mode, small text, filter resets and the Supply complaints are single-handler or minor.

## The wiki conversation (4.2 page comments)

- 14 Aug, Marcus (EM) asked Wen Li: does the proximity change apply to responders who turn jobs down? "was it a decision or if it just fell out that way". Wen Li: away until the 24th. No answer on the page since. (document)
- 18 Aug, Support lead: tickets about 3x, two themes; the ping-gone one is explained by the 60s wait, the phone-never-goes-off one is not. (document)
- 19 Aug, Priya: "seasonal". 26 Aug, Marcus: "That'll be the August dip." Our data does not support seasonal as the main cause.
- 28 Aug, Marcus: "I don't want to hand them a conclusion." 28 Aug, Wen Li: "Message me directly if something needs me." (document)
- Wen Li (Staff Engineer, Berlin), Marcus (Engineering Manager) and Helen (Director of Product) are three different people.

## Mechanism (guess, not confirmed)

The 90s to 60s wait turned slow answers into misses. The scoring (from code reading, offer.py and history.py) penalises a miss like a decline (0.12 against 0.08 credit, no decay), and proximity weight rose to 0.60 (acceptance 0.25). Rank fell, pings fell, and there was no way back. Not tested: that the four are slower responders (no response-time data) and that the loop is what happened (nobody has replayed the scores).

## Colleague comparison

Agree on cause and timing. Colleague states the loop and "slow responders" as fact, and "driven by" for the ping tickets. Those are guesses or only half-true. Colleague's supported extras: all 16 responders had misses; 80% home-area before 4.2; out-of-area misses.

## Open questions and next steps

1. Were any of the 23 callouts that ended on a missed ping actually unfilled? (Marcus, Wen Li)
2. Wen Li: replay stored scores for the four, with The Gale as the control, and answer Marcus's 14 Aug question.
3. Response-time data for the 60s against 90s question (Ravi or Wen Li).
4. Ravi's official weekly acceptance numbers; prior-year July to September.
5. Reply to the open ping tickets, starting with Pruitt and Okafor (Nadia owns the queue).
6. Talk to Helen about which squeezed-out Q3 items remain commitments, and options: different wait, a miss penalty that decays, or rollback.
7. Why the four had such high miss shares in their first days.

## The three Module 2 prompts

1. Who filed the ping-related tickets (ping gone and quiet)? Names, ticket counts, responder, first-ticket date, and ping tickets per week.
2. Check each handler's quoted ping count in the quiet tickets against the pings table for that responder and week.
3. Test Corporal Ashgrove and Halfmoon (not among the four) before and after 12 Aug, and check whether anyone else shows the same pattern.

## Checks before the summary (13 Oct)

- The 60s wait is visible in the data: after a missed ping the next ping went out 91 to 93 seconds later up to 8 Aug, and 61 to 63 seconds later from 12 Aug 09:04. (data)
- Declines (turned down) always came within 6 to 40 seconds, median about 22, both before and after 4.2. We cannot see how long takes took. So "slow responders" is not supported by the one response-time clue we have; treat it as untested, and possibly weak. (data; gap)
- In-area pings alone went from 0.7% missed to 10.3% missed, so the miss rise is not only responders being pinged out of area. (data)
- Callouts fell from about 140 a week to 110 in the week of 10 Aug, then 121 to 127 (about -13%), starting on 12 Aug itself, with 12 to 13 a day on 12, 13, 15 and 16 Aug against 14 to 27 before. Pings per callout rose from about 1.24 to 1.31. Unexplained: why callout volume dropped on release day. Ask Ravi or Marcus. (data; open)
- Tables are clean: every callout has at least one ping, no orphan pings, no unknown responders, no repeat pings to one responder within a callout.
- Still missing: response times for taken pings, capability tags, a callout outcome column, routing scores, ticket replies, prior-year data, and data after 7 Sep.

## Code read this session (config.py, history.py, offer.py, routing.py, availability.py)

- Timeout 60s (was 90). Weights: proximity 0.60 (was 0.45), recent acceptance 0.25 (was 0.40), capability 0.15. (config.py, document)
- A missed ping and a decline are treated the same: score -0.12, a take +0.08, no decay (2019 TODO), floor 0, start 0.5. (history.py, offer.py)
- Ranking only orders; nobody is removed. Dispatch returns None when the list runs out without a yes. Availability is set by the responder or handler; routing never changes it.
- The reweight lowers the cost of a decline (0.40 x 0.12 = 0.048 down to 0.25 x 0.12 = 0.030 of score). A 5-miss streak costs about 0.15 of score, worth about 11 minutes of travel time. So the loop only collapses a responder whose travel-time edge over neighbours was small. Needs travel times.

## Answers to "what I'd do differently" (13 Oct)

1. Was anyone left without cover? Probably yes, unconfirmed. By the code, a callout with no taker means the list ran out. Callouts with no taker: about 7 a week before 12 Aug, then 14, 17, 16, 7 in the following weeks. Callouts ending on a missed ping: about 0 a week before, then 6, 7, 6, 5. Whether they were handled another way is not in the database. (data; outcome unknown) Ask Marcus.
2. Response times? Not in the database for taken pings. Closest clue: decline times, median 22 to 23s, 90th percentile 33 to 39s, max 40s, the same for the four and for everyone else, before and after 4.2. So the four were not slower at declining. (data; gap) Ask Wen Li or Ravi for acknowledgement times.
3. Was the proximity change meant to apply to decliners? The code applies it to everyone equally; the release note says proximity is weighted more heavily relative to recent acceptance history; the roadmap item is silent. Marcus asked on 14 Aug and nobody has answered. The reweight actually softens the decline penalty, so decliners were not hit harder by it. Intent: ask Wen Li. (document and code; intent unknown)

## Final read (13 Oct)

4.2 changed the ping wait (90s to 60s) and the weights together. More pings expired, and the scoring (miss = decline, no decay) is the likely reason four responders (Farlight, The Undertow, Vesper, Meteor Mite) fell from about 49 pings a week to about 3 while ten others gained. Confident: the timeout and weight changes, the timing, the miss-as-decline code. Likely: the scoring caused the collapse. Not explained: why the four missed 44 to 63% of pings in their first days when their decline times look normal. Most urgent: confirm whether callouts went unfilled. Contradiction tests passed so far: the drop was gradual not instant, in-area misses also rose, and Meteor Mite fell while The Gale (same area) rose.
Next: Marcus (unfilled callouts, 14 Aug question, callout drop on 12 Aug), Wen Li (score and travel-time replay, ack times, decay intent), Ravi (official weekly numbers, prior year), Nadia (ticket replies), then Helen with options.

## Score reconstruction from the pings table (13 Oct, no engineer needed)

Rebuilt each responder's recent-acceptance score using the history.py rules (start 0.5, +0.08 taken, -0.12 missed or declined, floor 0, ceiling 1) over every ping. Covers only the acceptance part (weight 0.25), not travel time or availability. (data plus code rules; reconstruction, not production scores)

- Before 12 Aug every responder sat at 0.80 to 1.00, including the four (Farlight 0.84, The Undertow 0.88, Vesper 0.96, Meteor Mite 1.00). So their old history was not the problem, and Meteor Mite's higher pre-4.2 decline rate did not lower its score.
- After 12 Aug the four fell to 0: first below 0.3 on 17 Aug (Undertow), 19 Aug (Farlight), 22 Aug (Meteor Mite), 23 Aug (Vesper), about when their pings thinned. None recovered.
- The other twelve never fell below 0.44, except Nightwell, which dipped to 0.28 on 18 Aug and recovered to 0.88 because it kept getting pings. Recovery works if pings continue; the four stopped getting pings.
- Still needs engineering: travel times and availability, to show the lower score actually moved them down the order, and why Nightwell kept getting pings at 0.28. The collapse needs the four's proximity edge to be small.
- Upgrade: the score side of the mechanism is now supported by data, not just by code reading. The ranking side is still unconfirmed.

## Documentation search for the three unexplained items (13 Oct)

Read: Rook Dispatch one-pager, Glossary, 4.1 and 4.2 pages, Availability Confidence, Research, team directory pages, Priya's handoff, and the routing code. None explains the three items directly.

- Miss-as-decline is documented behaviour, not a hidden bug. Glossary: "Turning down or missing a ping lowers the recent-acceptance component, which lowers the responder's place in the order for later callouts." (document)
- No documented rationale or response-time analysis for the 60s wait. Roadmap item says only "Tune how long a ping waits"; 4.2 says "Pings that go unanswered move to the next responder sooner." Handoff admits two things moved at once. (document; gap)
- Intent vs outcome: the handoff says the proximity change was for responders who were unhappy that "someone nearby could sit unoffered while the system reached for someone with a better acceptance record forty minutes away." But the home-area share of first pings fell from 80% to 61% after 4.2, the opposite of that intent. (document against data) Ask Wen Li.
- 4.1 (16 Jun) switched proximity to a travel-time estimate and 4.2 then weighted it more heavily. Nothing documents how accurate the estimate is. (document; lead, not a finding)
- Callout drop on 12 Aug: no documentation. Only claim is Priya's "August is always soft for us, every year", untestable without prior-year data. Incidents can come from "an intake system", which could also matter. Ask Ravi and Marcus. (document; unverified)
- No written description of who-gets-pinged exists: "it's a conversation with her, not a document". Priya asked the new PM to write it.

## Second wiki pass (13 Oct): where the answers would be

Read the Q3 roadmap, Releases, Team directory, About Rook, Rook Supply, the briefs and the people pages. The wiki does not answer the open questions, but it points to where the answers sit.

- Response times: Dispatch tracks time-to-accept (median seconds from ping sent to taken) alongside acceptance rate, and Ravi "reports weekly on how often responders are taking their pings". Ask Ravi for weekly time-to-accept before and after 12 Aug. (document)
- Handler overrides: Dispatch lets handlers override routing, and 4.0 added an audit log of every override (who, when, which responder instead). Not in rook-database. Ask Marcus to pull it from 12 Aug: overrides could explain callouts bypassing the four. (document; untested lead)
- Unfilled callouts: Glossary separates a coverage gap ("nobody could have gone") from low acceptance ("nobody would"). The pings table cannot tell which the 49 no-taker callouts were. (document; gap)
- Wen Li: the directory (updated 2 Sep) lists them away only 14 to 24 Aug and they posted on 28 Aug that they were back. The README's fallback if they are out is the engineering manager. (document)
- Process: the roadmap says changes to a committed item go through Product; config.py says not to change values without telling the engineering manager. "Ping timeout tuning" and "Change to who gets pinged" are both Committed for 4.2. (document)
- Supply reads the availability record Dispatch writes and schedules maintenance into low-callout windows, so quiet responders could get maintenance booked into their windows. A possible knock-on, unchecked. (document; guess)
- Callout drop on 12 Aug, travel-time accuracy: still nothing in the wiki.
