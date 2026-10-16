# 05 · Super Speed — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. You've spent three sessions finding out what went
wrong: the two piles of feedback that didn't agree, the numbers that
hid four people inside an average, and the code that settled it —
the shorter timeout is what did it.

At the end of the session, type wrap up, and Claude Code saves the
prompts you wrote yourself below — not the starter prompt — updates
CLAUDE.md, and saves your work to GitHub. By Module 6 this file is a
prompt library built from your own questions.

---

### 1.

Read 05-super-speed/director-request.txt, the rook-wiki Glossary and Team directory, the 4.2 release comments, and 00-rook/company/notes/handoff-from-priya.docx. Then write a brief that answers exactly what Helen is asking for.

Length: 2 pages at most. It must be clear and easy to understand for someone who has not read the details. Use plain English, short sentences, and real names from the Team directory.

Ground it in The Undertow, the responder I followed in Module 3.

The brief must include:
- Summary: the problem in 3 sentences
- Who it is for
- What changes for them once it exists
- Solution: the proposed fix and what it deliberately does not do
- Timeline: the steps, who owns each one, and rough dates. Mark any date that is a guess as "proposed."
- The problem: the 4.2 wait went from 90 to 60 seconds, a missed ping counts like a decline, and the score never recovers
- What is confirmed, likely, and unknown
- Who I need to ask, and what success looks like

Do not make up facts. If something is not in the files or the data, say it is unknown. For the solution and timeline, give options and say what each one depends on.

### 2.

We are going to explore solutions for this problem: once a responder's score drops, they are very unlikely to get enough pings to raise it again. Review the project files from 04 and earlier, 05-super-speed/director-request.txt, the rook-wiki Glossary, Team directory and 4.2 release comments, and 00-rook/company/notes/handoff-from-priya.docx. Tell me if anything in the problem is unclear.

Context from my work: in 4.2 the wait went from 90 to 60 seconds, a missed ping costs the same as a decline (0.12), a taken ping adds 0.08, and the score never recovers. I followed The Undertow in Module 3. Engineering could quietly revert the timeout, but Helen wants something that still works for the responder with the faster window, built from the responder's point of view.

Ideas to include: a handler can weigh in on a miss (for example, "that was legitimate, do not penalize"), and a miss should be treated differently from a turn-down.

Do not write the brief yet. Propose features in three groups: (1) for the responder only, (2) for the responder and handler, (3) data and logging improvements. Give each a rough t-shirt size (S, M, L). Base sizes only on what is in the files, and mark any size that is a guess. Say what each feature depends on and what is unknown. Do not make up facts.

### 3.

do you agree with this?

I see three layers:

1. The trigger: the wait went from 90 to 60 seconds, so more pings are missed. That is confirmed in the config and the data.
2. The trap: a miss counts like a decline, and the score never recovers. A responder who falls behind rarely gets offered pings, so they cannot earn their way back. This is likely, but nobody has replayed the real scores.
3. The blind spot: when a miss happens on a short list, the callout can end with no taker and no retry. This is the customer risk. It is the least understood and the most serious.

My main worry is layer 3. Layers 1 and 2 hurt responders. Layer 3 may hurt customers.

The solution: I would do it in this order:

1. Check the unfilled callouts first. Ask Marcus. If any went unfilled, that comes before everything else.
2. Fresh start for the four. This is the quickest way to help The Undertow. Cheaper misses alone will not help someone already at the bottom.
3. Separate misses from turn-downs. A turn-down is a choice. A miss may be a timing problem, so it should cost less.
4. Let handlers flag a miss as legitimate. It is useful, but it adds work for handlers and depends on them noticing. I would keep it as a second step.
5. Better logging. Weekly pings per responder against their own baseline would have caught this days earlier than the tickets did.

What I would not do:

* Revert the wait quietly. We do not yet know if the wait is the whole cause, and Helen asked for something that works with the faster window.
* Promise a fix before Wen Li replays the scores.

What would change my mind: if the replay shows the four's scores were not low, the score-loop idea is wrong, and the plan needs rethinking.

### 4.

this is what we are going to work on for now just remember and then i will share prompt

### 5.

also add that i like it to be 2 pages no longer clear to understand

### 6.

can you provide me here with thte breef for me to read and then we when good we pill pust it to gip

### 7.

now sumarize eerything and write me a brief

### 8.

also read this pls

### 9.

now ok great can you write me the brief

### 10.

show me here so i can read it befroe we push it

### 11.

Save the brief exactly as it stands now as 05-super-speed/brief.md. Show me the file when it's done.

### 12.

rewrite the breef so it is not for helen pls and save the new version in the md file

### 13.

also i dont see the 3 promps saved into my file can you list me the 3 promps

### 14.

save the prompt to 05-super-speed/prompts.md and also the promos into the files

### 15.

where i can see the prototip

### 16.

Improve prototype.html. Do not change the features. Make it look cleaner and easier to understand for a handler who has 10 seconds:
- Put a clear headline at the top: "The Undertow has gone quiet" with the numbers (1 ping this week, was about 12).
- Make "Give a fresh start" and "Mark as legitimate" the two most visible buttons.
- Show misses and turn-downs in separate colors with a short label.
- Use more white space, bigger text, and shorter lines.
- Make the Responder phone tab look like a narrow phone screen with one message and one button.
- Add a small label: "Prototype. Example data."
After the changes, tell me exactly what you changed and what you could not test.

### 17.

what else would you make better on the prototipe

### 18.

ok imrove and update the prototype

### 19.

the demo we build  what i am looking at who is the viewer can you remind me

### 20.

what about the view as responder and see as handeler and i wasnt to see more then one person like 3 and also i want to see phase as a handeler and show me web and mobile

### 21.

is what we have aline with this

Update 05-super-speed/prototype.html. Keep it one file with example data only. Do not change what the brief says. Make it clean and easy to understand in 10 seconds.

HANDLER VIEW
- Start with a "Sign in as" picker showing 3 handlers: Desmond Okafor, Pruitt, and Kip.
- After I pick one, show only that handler's own screen. Never show the others.
- Okafor sees The Undertow. Pruitt sees Farlight. Kip sees Meteor Mite and The Gale.
- Add a "Switch handler" button.
- At the top of a quiet responder, show a plain headline, for example: "The Undertow has gone quiet. 1 ping this week, was about 12."
- Show misses and turn-downs separately, in two colors, with a short label.
- Show the last 8 pings for that responder.
- Two large buttons: "Give a fresh start" and "Mark this miss as legitimate."
- After a button is clicked, show a clear change: the counted misses go down, or a green banner says the fresh start was given.

RESPONDER VIEW
- A narrow phone-style screen for the selected responder.
- One short plain message explaining why pings dropped, and one button: "Ask my handler to restart."
- After the button is clicked, show a confirmation message.

STYLE
- More white space, bigger text, short lines.
- One main color, one warning color.
- A small label on every screen: "Prototype. Example data."
- No blame in the wording. Keep it neutral and plain.

RULES
- Use real numbers only for The Undertow (12 pings a week before, 1 after, 11 open tickets). For all other responders, mark the numbers as "example."
- Do not invent features, names, or data that are not in the files or in the brief.

When finished, tell me exactly what you changed and what you could not test. Do not commit yet.

### 22.

can you create me a new prototipe

### 23.

lets try this

Update 05-super-speed/prototype.html. Keep it one file. Keep the details from the original prototype (number of pings, the responder's name, and their area), and add the changes below. Do not change what the brief says.

DATA
- Use the rook-database pings table for real numbers and rows where you can. Where something is not in the data or files, label it "example." Do not invent facts.
- Responders, areas, and handlers (from our data): The Undertow, Harborside, Desmond Okafor. Farlight, Uptown, Pruitt. Meteor Mite and The Gale, Eastgate, Kip. Vesper, Old Town, Aunt Dot.
- For each responder show: name, area, handler, pings per week before and after 12 Aug, taken, turned down, missed (as separate numbers), and the missed rate before and after.

HANDLER VIEW
- Start with a "Sign in as" picker showing 3 handlers: Desmond Okafor, Pruitt, and Kip.
- After I pick one, show only that handler's own screen. Never show the other handlers' responders.
- Add a "Switch handler" button.
- For each responder, show a card with the details above and a "gone quiet" flag if pings dropped a lot.
- Click a responder to open their detail: a weekly table (pings, taken, turned down, missed), their last 8 pings with date, time, area, and outcome, and the open tickets count for The Undertow (11).
- Two large buttons on a quiet responder: "Give a fresh start" and "Mark this miss as legitimate."
- After a click, show a clear change: counted misses go down, or a green banner says the fresh start was given.
- Headline example: "The Undertow has gone quiet. 1 ping this week, was about 12."

RESPONDER VIEW
- A narrow phone-style screen for the selected responder, showing their name and area.
- One short plain message about why pings dropped, and one button: "Ask my handler to restart."
- After a click, show a confirmation message.

STYLE
- Clean layout, more white space, bigger text, short lines.
- One main color, one warning color, and separate colors for misses and turn-downs.
- A small label on every screen: "Prototype. Example data where marked."
- Neutral wording. No blame.

RULES
- Do not invent features, names, or numbers. Do not use first names for Pruitt or Kip unless they are in the Team directory.
- Do not commit yet.

When finished, tell me exactly what you changed and what you could not test.

### 24.

Rebuild 05-super-speed/prototype.html as one single file. Keep it clean, visual, and easy to understand in 10 seconds. Use real data from the rook-database pings table wherever it exists. Where something is not in the data or the files, label it "Example only." Do not invent facts, names, numbers, or features. Do not commit yet.

TWO TABS AT THE TOP
- "Handler console" and "Responder phone."
- A small label on every screen: "Prototype. Example data where marked."

HANDLER CONSOLE
Left menu: Callouts, My responders, Routing overrides, Reports (only "My responders" needs to work).

1. Sign in as: a picker with 3 handlers: Desmond Okafor, Pruitt, and Kip. After choosing, show only that handler's own responders. Add a "Switch handler" button.
   - Okafor: The Undertow (Harborside). Pruitt: Farlight (Uptown). Kip: Meteor Mite and The Gale (Eastgate).
   - Use only names and areas from the data and files. Do not invent first names.

2. "My responders" list: one card per responder with name, area, pings per week before and after 12 Aug, taken, turned down and missed shown separately, the missed rate before and after, and a "Gone quiet" or "Normal" flag.

3. Click a responder to open the detail screen:
   - Name, area, handler, and a banner. Example: "The Undertow has gone quiet. 1 ping this week, was about 12."
   - A small weekly table: pings, taken, turned down, missed.
   - "Last 8 pings": callout number, date and time, and result as a colored label. Green = Taken (they said yes). Purple = Turned down (they said no). Red = Missed (ran out of time).
   - A "Mark as legitimate" button on each missed row. After clicking, that miss stops counting, and the line "X of the last 8 count as misses" updates.
   - A "Give a fresh start" button. After clicking, show a green banner: "Fresh start given. Dispatch will offer [name] callouts again. Watch the next 2 weeks: pings per week, misses, unfilled callouts."
   - A "My responders" back link.
   - Show "11 open ping tickets" for The Undertow only, from the tickets table.
   - Responders who are not quiet show a normal status and no fresh start offer.

RESPONDER PHONE
A narrow phone-style screen for the selected responder:
- Name, area, and handler at the top.
- A status card in plain words: "You had 1 ping this week. Before, it was about 12."
- "My past pings": the last 8 pings with date, time, area, and colored result labels. If a miss was marked legitimate, show "Your handler marked this as okay."
- "Coming up": do not list future callouts, because no such data exists. Show: "New pings arrive live when a callout is near you."
- One plain message: "A missed ping used to count like saying no. This is changing."
- One button: "Ask my handler to restart." After clicking, show: "Your handler has been asked."

STYLE
- Clean layout, more white space, larger text, short lines.
- One main color (blue), one warning color, and the three result colors above.
- Neutral wording. No blame.

WHEN FINISHED
Tell me exactly what you changed, which numbers are real, which are labeled "Example only," and what you could not test.

### 25.

lets update the handelar part based on this

HANDLER CONSOLE (rewrite)
Left menu: Callouts, My team, Routing overrides, Reports (only "My team" needs to work).

1. Sign in as: a picker with 3 handlers: Desmond Okafor, Pruitt, and Kip. After choosing, show that handler's team. Add a "Switch handler" button.
   - Okafor: The Undertow (Harborside). Pruitt: Farlight (Uptown). Kip: Meteor Mite and The Gale (Eastgate).
   - Use only names and areas from the data and files. Do not invent first names.

2. My team table, ranked from best to lowest:
   - Rank by taken rate since 12 Aug (taken pings divided by all pings). Show the rank number. Break ties by missed rate (lower is better).
   - A toggle at the top: "My team" and "All 16 responders." The default is "My team."
   - One row per responder with the same details the responder sees: name, area, handler, pings per week before and after 12 Aug, taken, turned down, and missed shown separately, the missed rate before and after, the date of their last taken ping, and a "Gone quiet" or "Normal" flag.
   - Use colored labels: green for taken, purple for turned down, red for missed.
   - Gone quiet rows get a warning color.

3. Click a responder to open the same detail screen the responder sees:
   - Name, area, handler, and a banner. Example: "The Undertow has gone quiet. 1 ping this week, was about 12."
   - A small weekly table: pings, taken, turned down, missed.
   - "Last 8 pings" with callout number, date and time, and a colored result label.
   - A "Mark as legitimate" button on each missed row. After clicking, that miss stops counting, and "X of the last 8 count as misses" updates.
   - A "Give a fresh start" button. After clicking, show a green banner: "Fresh start given. Dispatch will offer [name] callouts again. Watch the next 2 weeks: pings per week, misses, unfilled callouts."
   - A back link to "My team."
   - Show "11 open ping tickets" for The Undertow only.
   - Not-quiet responders show a normal status and no fresh start offer.

Use real rows and numbers from the rook-database pings table. Label anything not in the data "Example only." Do not invent facts. Do not commit yet. When finished, tell me what you changed and what you could not test.

### 26.

give me the final url

### 27.

go to this verson for handelor file:///C:/Users/mbourgeois/claude-code-for-pms-final/05-super-speed/prototype.html

### 28.

HANDLER CONSOLE (rewrite: one dashboard screen, all responders visible at once)
Left menu: Callouts, My team, Routing overrides, Reports (only "My team" needs to work).

1. Sign in as: a picker with 3 handlers: Desmond Okafor, Pruitt, and Kip. Add a "Switch handler" button.
   - Okafor: The Undertow (Harborside). Pruitt: Farlight (Uptown). Kip: Meteor Mite and The Gale (Eastgate).
   - A toggle: "My team" and "All 16 responders." Default is "All 16 responders," so the dashboard has a full ranking.
   - Use only names and areas from the data and files. Do not invent first names.

2. Top summary bar: total responders, how many "Gone quiet," how many "Normal," overall missed rate before and after 12 Aug.

3. One dashboard, a ranked table with one row per responder, all visible on one screen without clicking:
   - Rank from best to lowest by taken rate since 12 Aug. Break ties by lower missed rate.
   - Columns: rank, name, area, handler, status flag ("Gone quiet" in warning color or "Normal"), pings per week before and after 12 Aug, taken, turned down, and missed as separate numbers, missed rate before and after, and the date of the last taken ping.
   - A small weekly bar chart in each row (from 29 Jun to 6 Sep), showing pings per week, with a marker at 12 Aug.
   - A "Last 8 pings" strip of 8 colored dots in each row. Green = Taken, purple = Turned down, red = Missed. Hover shows callout number, date, and time.
   - Color the row edge to match status: warning color for quiet, none for normal.
   - Rows for quiet responders have two buttons: "Mark a miss as legitimate" and "Give a fresh start."

4. Actions without leaving the dashboard:
   - "Mark a miss as legitimate" opens a small panel listing that responder's missed pings from the last 8. Each has a button. After clicking, that dot changes to a "legitimate" style, and the missed count updates.
   - "Give a fresh start" shows a green banner on that row: "Fresh start given. Dispatch will offer [name] callouts again. Watch the next 2 weeks: pings per week, misses, unfilled callouts."

5. Keep it easy to scan: compact rows, clear spacing, a sticky header and column titles, and a legend for the three result colors.

Show "11 open ping tickets" for The Undertow only. Use real rows and numbers from the rook-database pings table. Label anything not in the data "Example only." Do not invent facts. Do not commit yet. When finished, tell me what you changed and what you could not test.

### 29.

i dont like the visual at all  i want the for handler to see the list of all reporters and then when i clic ai want to see all the call location like we did before rewrite

### 30.

the handelor console i need have the responder name the area the pings for the week ans status then when i click on the fresh start given i wasn to see deatls of that person loast 8 pins with claaut id, when results missed taken turn donw and and then graff which will show me his or her perfomcae like we did here

### 31.

bring my prototipe to this verson file:///C:/Users/mbourgeois/claude-code-for-pms-final/05-super-speed/prototype.html

### 32.

give me my second promt for the prototipe

### 33.

udate this part HANDLER VIEW - Start with a "Sign in as" picker showing 3 handlers: Desmond Okafor, Pruitt, and Kip. - After I pick one, show only that handler's own screen, never the others. - Okafor sees The Undertow. Pruitt sees Farlight. Kip sees Meteor Mite and The Gale. - Add a "Switch handler" button. - At the top of a quiet responder, show a plain headline, for example: "The Undertow has gone quiet. 1 ping this week, was about 12." - Show misses and turn-downs separately, in two colors, with a short label. - Show the last 8 pings for that responder. - Two large buttons: "Give a fresh start" and "Mark this miss as legitimate." - After a button is clicked, show a clear change: the counted misses go down, or a green banner says the fresh start was given.

### 34.

i dont see the routing overrides any infomation pls update that part

### 35.

in buttom my team i wasnt to have more infomation for each responder to see data calls location

### 36.

in the view for my team i want to see for each responder all the details and be coloered from t the top of a quiet responder, show a plain headline, for example: "The Undertow has gone quiet. 1 ping this week, was about 12." - Show misses and turn-downs separately, in two colors, with a short label. - Show the last 8 pings for that responder. - Two large buttons: "Give a fresh start" and "Mark this miss as legitimate." - After a button is clicked, show a clear change: the counted misses go down, or a green banner says the fresh start was given.

### 37.

THEME: SUPERHERO TEAM (replace the STYLE section; keep all data rules)

Naming (labels only, same features):
- "My responders" becomes "My Hero Team."
- "Routing overview" becomes "Mission Control."
- "Reports" becomes "Mission Reports."
- "Gone quiet" becomes "Gone quiet" with a small shield icon. Keep the plain words, so nothing is unclear.
- "Give a fresh start" becomes "Give a fresh start" with a small bolt icon.
- Keep "Taken," "Turned down," and "Missed" exactly as they are, so the data stays clear.

Look:
- Dark navy background, white cards, bright electric blue as the main color, gold for highlights, red for Missed, purple for Turned down, green for Taken.
- Bold headlines, rounded cards, and a small badge or shield icon on each responder card (original shapes, simple icons only).
- Rank shown as a medal-style number: gold for 1st, silver for 2nd, bronze for 3rd, plain for the rest.
- "Gone quiet" responders get a soft glowing red edge on the card.
- On the Responder phone tab, a "Hero Mode" header with the responder's name and area, and the same narrow phone layout.
- Small label on every screen: "Prototype. Example data where marked."

Tone:
- Fun in the headers, plain in the details. Do not joke about missed pings or about anyone who has gone quiet. Keep the wording neutral and respectful.
- Do not draw or name any existing superhero, character, logo, or brand.
- Readability comes first: large text, strong contrast, no clutter.