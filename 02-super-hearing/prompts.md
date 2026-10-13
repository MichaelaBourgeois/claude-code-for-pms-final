# 02 · Super Hearing — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. Last session you built a context file and met the
company.

You still do not know what actually went wrong.

At the end of the session, type wrap up, and Claude Code saves the
prompts you wrote yourself below — not the starter prompt — updates
CLAUDE.md, and saves your work to GitHub. By Module 6 this file is a
prompt library built from your own questions.

---

### 1.

promts 1 Go through the four interviews. For each theme, tell me whether the handler raised it on their own or after a question from the designer. Quote the line and the question before it. Then tell me which themes still hold using only the unprompted statements.

### 2.

prompt 2 Handlers for Captain Vantage and Sgt. Bulwark report callouts going to someone else, but their responders are not among the four hit responders. Using rook-database, check their ping history week by week, before and after 12 Aug. Show taken, turned down, and missed counts, and tell me whether the data matches what the handlers said.

### 3.

prompt 3 Across the four interviews, what did only one handler say, and what do handlers say that contradicts each other or the ping data? For each point, label it as supported by a quote or only a guess, and tell me what I would need to check to confirm it

### 4.

sumarize all the finding and let me know what whent wrong in 4.2 relase in your opinion

### 5.

i need 2 senteses what was the trbale with 4.2

### 6.

do you think this is correct / Based on the interviews and ping data, the trouble with 4.2 is that pings expire faster (60s), and missed pings lower a responder’s score with no way to recover, so some responders get far fewer pings and nobody can see why

### 7.

Prompt 1: Who filed them, and when did it start?
Who filed the ping-related tickets (ping gone and quiet)? Give me a list of names, how many tickets each person filed, which responder it was about, and the date of their first ticket. Then tell me how many ping tickets came in each week

### 8.

Prompt 2: Check what handlers claim against the data
In the quiet tickets, handlers quote their own ping counts, for example ‘four pings in the past seven days, usually about twelve.’ Check each claim against the pings table for that responder and week. Tell me which claims match, which do not, and quote the ticket

### 9.

Prompt 3: Test the responders who were not on my list
Corporal Ashgrove and Halfmoon filed quiet tickets but are not among the four hit responders. Using rook-database, show their weekly pings, taken, turned down, and missed counts, before and after 12 Aug. Do they fit the same pattern as Farlight and The Undertow? Also tell me whether anyone else not on my list shows the same pattern.

### 10.

after all this provide me a visual summary

### 11.

ok what is your view of this issue

### 12.

is it the same as me?

### 13.

who is write and who is wrong

### 14.

did i ask the wrong questions?

### 15.

will i still solve the issue?

### 16.

is there some conversation you can find?  Wen li is not her or marcus

### 17.

If both piles are telling the truth, how can they both be right?

### 18.

ok cheikc anyting else you need to kow before we come to a sumary of these findings? What to check: The ping data is the tiebreaker, because it records what happened without depending on who chooses to speak or file.

### 19.

if you comapre my first summary of the problem and summary now is there diffrence?

### 20.

Prompt 1: Which pile to trust
For each topic where the interviews and tickets disagree, tell me which pile I should trust and why. Use the ping data as the tiebreaker. For each one, label it as supported by data, supported only by a quote, or a guess.

### 21.

Prompt 2: What would I have got wrong?
If I had only read the interviews, what would I have got wrong about 4.2? If I had only read the tickets, what would I have got wrong? Quote one line from each pile to show it

### 22.

Prompt 3: What would prove me wrong, and what is next?
My current read is that 4.2’s shorter ping wait caused more missed pings, and the scoring then left some responders with almost no pings. What evidence in the interviews, tickets, or ping data would contradict that read? What is the strongest alternative explanation? Then split everything into confirmed, likely, and unknown, and tell me what I need to confirm, who I should ask, and what the next steps are

### 23.

ok what is your final visiont what whent wrong did i ask the right questions?

### 24.

do you have now clear vision what happened based on reading the interviews ticket comparing everything? do we have clear path moving forward?

### 25.

when you compare my original note what is wrong after this what is the 2 sentence summary what need to be fixed

### 26.

but this isn’t confirmed until Wen Li replays the scores, is this possible you know she is not here a

### 27.

so what is the final summary

### 28.

do you see any documentation for this? try to find

### 29.

if you have question pls go to wiki and try to find any answr you need before you provide me with final answer pls and then give me final answer

### 30.

can you comapre what we thought the orignal issue vs now

### 31.

can you now sumarize to me visually what is happening after looking at the interviews and tickets to understand the problem
