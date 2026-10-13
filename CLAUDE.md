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

I am the new Product Manager for **Rook Dispatch**, replacing Priya Raghunathan (left 21 Aug 2026). Sources: rook-wiki (About Rook, Glossary, Team directory, Releases, Q3 roadmap, Product briefs, 4.2 page comments) and `00-rook/company/notes/handoff-from-priya.docx`. Wiki last reviewed in this session: 13 Oct 2026.

### Products
- **Rook Dispatch** (mine): responder coordination. An incident arrives, Dispatch ranks available responders (routing priority), pings the top one's phone, and moves down the list on turned down / missed. Handlers use the web console; responders use the native phone app. Monthly release train, 4.x numbering. Routing config ships with the release; handlers can't change it at runtime.
- **Rook Supply**: gear provisioning (requisitions, maintenance, field failure reports) for handlers and quartermasters. Shares the Responder Availability Record with Dispatch (Dispatch writes, Supply reads).
- Customers are independent masked responders plus their handlers and quartermasters. Rook employs no responders. Pricing is per active responder.
- **Hard rule:** responder cover identities are never stored and we cannot map them to legal identities (contractual; Security Policy 4.1). Never design anything that assumes this mapping, and never try to work out who anyone is.

### People (wiki roles → names; comments and the handoff use roles only)
| Role in comments | Person | Notes |
| --- | --- | --- |
| Engineering manager | Marcus Oyelaran, Site Aleph | Runs Dispatch engineering; start here when unsure |
| Staff engineer | Wen Li, Berlin | Built the who-gets-pinged logic; no written spec exists; away 14–24 Aug |
| Support lead | Nadia Hoffmann, Berlin | Owns tickets; hears handler complaints first |
| Product designer | Sofia Marino, Site Aleph | Console and phone app; ran the September interviews |
| Director of Product | Helen Achebe, Site Aleph | My director; owns roadmap and commitments |
| Data analyst | Ravi Menon, Singapore | Owns the real weekly acceptance numbers (Priya's handoff said ask the EM; Ravi is the source) |
| Priya | Priya Raghunathan | Predecessor, gone; owner of every roadmap item |

Handlers named in the wiki: Halloran (Sgt. Bulwark; Supply-side asks), Aunt Dot (Vesper), Mr. Ambrose (Captain Vantage), Kip (Meteor Mite, The Gale).

### Vocabulary
- **Callout**: request for a responder to attend an incident. **Ping**: one callout offered to one responder. **Taken / turned down / missed** (missed = ping wait expired; recorded separately from turned down, both move the ping on).
- **Ping wait**: seconds before a ping counts as missed. Same for everyone.
- **Acceptance rate**: share of pings taken. Headline metric. **Time-to-accept**: median seconds, ping sent to taken. **Coverage gap**: no available responder had the required capability tags (nobody *could*, vs. nobody *would*).
- **Routing priority**: score ranking responders; inputs are proximity (travel-time estimate), availability, capability match, recent acceptance history. Turning down or missing pings lowers the recent-acceptance part and so the responder's place in later orders.
- **Capability tags**: flight, structural-entry, hazmat-tolerant, cold-weather, aquatic, crowd-management, de-escalation. **Mutual aid**: cross-area cover, unsupported, Q4 exploration.
- Supply: **requisition**, **field failure report**, **service interval**.

### Releases
- 4.0 (7 Apr): console nav, responder profile redesign, routing override audit log.
- 4.1 (16 Jun): proximity as travel-time estimate, bulk callout, push reliability.
- 4.2 (12 Aug): proximity weighted up vs. recent acceptance; ping wait 90s to 60s; console filters persist; three defect fixes.

### Where things stand (the 4.2 problem)
- Support lead's split (26 Aug): ~two-thirds "phone never goes off", one-third "ping gone before I could answer". Priya and the EM say it's an August seasonal dip. The data (rook-database, 29 Jun-7 Sep) does not support that as the main cause:
  - Weekly acceptance held at 75-78% for six weeks, then 54% in 4.2's week (12 Aug), then 66, 67, 73%. Missed pings: ~2% before, ~14% after. Turned down didn't rise (21% to 18%). Tickets: 5-8 a week, then 20, 27, 32, 25.
  - Callout volume did fall ~15% (138/wk to 110-127), so some softness is real. Prior-year data is not in the database, so "every year" is unverified.
  - Farlight, Meteor Mite, The Undertow and Vesper went from ~49 pings/wk combined to ~3 by end of Aug; acceptance 75% to 23%, 59% of their remaining pings missed. They declined at the same rate as others before 4.2. The 60s cut also raised misses for everyone else.
- Leading hypothesis (**mechanism inferred from code, unconfirmed**): `offer.py` treats missed like turned down; `history.py` penalizes 0.12 per decline vs 0.08 credit, with no decay (2019 TODO); `config.py` cut the timeout 90s to 60s and moved weights to proximity 0.60 / acceptance 0.25. Misses lower rank, fewer pings, no chance to recover. Needs Wen Li to replay stored scores and travel times for those four.
- Not supported: push failures (they were pinged and missed), wrong availability settings (handlers say it's set correctly).
- Open question from the EM (14 Aug, never answered): does the proximity change apply equally to responders who turn jobs down? Priya also said not to reopen 4.2 or discuss reverting. Don't inherit either conclusion; the EM said not to hand me one.
- Next: Wen Li on scores, travel times and why those four; Ravi's official weekly numbers; prior-year Jul-Sep; response-time data for the 60 vs 90s question. Nadia has the ticket breakdown.

### Roadmap (Q3 2026; all last reviewed 30 Jun, so stale; all owned by Priya)
| Item | Target | Status | Concern |
| --- | --- | --- | --- |
| Change to who gets pinged | 4.2 | Committed | Shipped |
| Ping timeout tuning | 4.2 | Committed | Roadmap says "tune"; shipped as one flat 90s to 60s cut for everyone. Confirm that was the intent |
| Availability Confidence | 4.2 | Committed | "Show a confidence score alongside a responder's stated availability." Not in 4.2 release notes or routing CHANGELOG; no code for it in `00-rook/code`. Display only, so unlikely to be the ping problem (untested) |
| Requisition approval chains | 4.3 | Committed | Supply; brief's scope has crept (see below) |
| Handler phone app | Q4 | Exploring | Sofia exploring; unstaffed |
| Shared cover between responders | Q4 | Exploring | |

Priya flagged that which squeezed-out items remain Q3 commitments has **not been discussed** with Helen. I need to have that conversation. Roadmap changes to committed items go through Product.

### Briefs (wiki "Product briefs")
- **Bulk Callout** (Jan): same callout to several responders at once. Listed as shipped in 4.1; brief still says nobody has picked it up and has no baseline. Check status.
- **Routing Override Audit Log** (Mar): shipped in 4.0 per Releases; brief says ready to build. Treat as stale.
- **Requisition Approval Chains** (Jul, Supply): core ask is a second approval over $2,000; the brief then piles on several unrelated features and leaves phasing open. Needs scoping.
- **Handler Phone App** (Sep): notifications, status view, one-tap contact; driven by one handler (Aunt Dot). Not staffed.

### Other handoff notes
- No written description of how who-gets-pinged works. Priya asked me to write it; get it from Wen Li.
- Filter-persistence tickets are noise. Console and mobile are stable; routing is where the risk is.
- Priya admits making calls "faster than I checked them"; question inherited assumptions in the first month.
- Tickets filed from inside an active callout bypass the support queue.
- Tools: rook-wiki (search_wiki searches titles only; read_page shows comments). rook-database tables: callouts, pings, responders, handlers, support_tickets (29 Jun–7 Sep 2026 only). Routing code is in `00-rook/code/dispatch-routing/` (config.py holds the weights and timeout).
- Handlers of the four hit responders: Linda Pruitt (Farlight), Desmond Okafor (The Undertow), Kip (Meteor Mite; also The Gale, who was not hit), Aunt Dot (Vesper). Good first calls, and Aunt Dot and Kip are already in the wiki's interview pile.
- Availability Confidence is display-only and absent from code and the 4.2 changelog, so probably unrelated to the ping drop; still unasked: was it meant to feed routing? Ask Helen, Marcus, Sofia.
- Database weeks start Monday; the 10 Aug week includes two pre-4.2 days, so use 12 Aug as the cutoff. Ticket volume is ~4x, not Nadia's "3x".
- How I want answers: quote the source for each claim, separate "supported by a document" from "only a guess", and say what data is missing. Treat Priya's and the EM's explanations as claims to test.
- Module 2 (13 Oct): missed pings rose for all 16 responders after 12 Aug (~2% to ~14%); the four collapsed, Ashgrove and Halfmoon fell about a quarter, the other ten gained 19-49% pings. The 60s wait shows in timestamps (next ping 91-93s after a miss until 8 Aug, 61-63s from 12 Aug). Declines always came within 6-40s for everyone, so "slow responders" is untested and weak; taken-ping response times are not in the database.
- Scores rebuilt from the pings table with the history.py rules show the four falling to 0 on 17-23 Aug while the others stayed above 0.44. That supports the miss-as-decline loop, but whether it moved them down the order still needs travel times and availability from engineering. The home-area share of first pings fell 80% to 61%, the opposite of the handoff's stated intent for the proximity change.
- Biggest risk: 49 of 440 callouts since 12 Aug (11%) have no recorded taker, against 48 of 879 (5.5%) before, and 23 ended on a missed ping. Ask Marcus whether any went unfilled. Callouts also fell ~13% starting exactly on 12 Aug, unexplained.
- Tickets: 147 in all; 46 ping tickets from 12 handlers (16 ping gone, 30 quiet), first on 12 Aug and 17 Aug, all post-12 Aug ones open at 7 Sep. Dot and Kip filed none. Filter tickets are 16 (11%), low severity, not noise; the console and account areas also have tickets. Interviews and tickets sample different people; trust the ping data for routing questions.
- Where answers sit: Ravi for time-to-accept before/after 12 Aug; Marcus for the routing override audit log (4.0), unfilled callouts and the 14 Aug question (code applies the change equally and the reweight softens the decline penalty; intent unknown); Wen Li for the travel-time replay (the wiki shows them back since 28 Aug; the README says ask Marcus if they are out). Full notes in `02-super-hearing/module-2-findings.md`.
