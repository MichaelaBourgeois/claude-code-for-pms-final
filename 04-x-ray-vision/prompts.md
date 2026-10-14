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

Has anything in this code changed recently? Walk me through what's different, and why it would matter to a responder.

### 2.

A callout has only one available responder, and they miss the ping. What does the code do next? Where in the code does that happen? Does it explain why most callouts with no recorded taker have only one ping?

### 3.

For each area, how many different responders have been pinged at all? For the 49 callouts since 12 Aug with no taker, how many were in areas where another responder has been pinged before? Show me the rows

### 4.

any notes you can find from wen li i am not able to talk to her she is not here

### 5.

this is what my group is posting just for comparasing

### 6.

any visualization after this exercise?

### 7.

my cowork can you create uml diagram?

### 8.

what is the final summary of this with no visual just give me very basic overview

### 9.

read this and run your data

### 10.

can you give me one senstend of the hypothesis here?

### 11.

where there any code changes since that 4.2 release that may have change anythign?

### 12.

did any open question that an enineer posted as a comment in the code somewhere?

### 13.

Are there any engineering comments in the codebase worth evaluating further

### 14.

what code changes were introduced in 4.2 that may be contributing towards the issues we've been seeing with more misses and less pings being sent

### 15.

sumarize so i can share one sentence if possible

### 16.

is this correct? Based on what I found, 4.2’s shorter wait caused more misses, and the code treats a miss as a decline with a tough recovery path, so a few responders were pushed down and rarely pinged again. The weight change may have concentrated on responders who had other close proximity responders, as this became a more heavily weighted metric.

### 17.

what about this Based on what I found, the reason some responders are getting no pings at all is that 4.2 combined a shorter wait (60 seconds instead of 90) with a heavier weighting on distance and a lighter weighting on track record. Responders who used to answer between 60 and 90 seconds, or who aren’t the nearest to their area’s callouts, now miss pings more often. Each miss lowers their score by more than a take raises it, and the score never recovers by itself. They drop down the ask-list, get fewer pings, and so get fewer chances to answer and climb back, while nearby responders pick up the work.

### 18.

can you find why? The 60-second wait and the weights applied to all 16. The other twelve missed more pings but recovered, while the four never did. Your version has no answer for why those four, and I’d say so openly.

### 19.

stop for now pls

did we covered this?

### 20.

does it look at who's been turning down jobs or just new onec and how that kind of affets the score?

### 21.

do we have answer fromthe engineering manager?

### 22.

now chaick the code agains the data

### 23.

any prompt i need to ask to solve this?

### 24.

run all the promts you need to find the soluton pls

### 25.

did the 3 promps helped you?

### 26.

ok provie me with your sumary what we know now comparing the tickets, interviews all the tables and now the code

### 27.

this is the sumary my collegue shared will you agree just curios

### 28.

fo we have an answer to this question? Quick one, did the change to who gets asked first apply to responders who'd already been turning jobs down, or just new ones? Can't tell from the code and don't want to guess on this. Anyone know?

### 29.

short version which i can share pls

### 30.

these were my collegues answers

### 31.

marcus is the manager?

### 32.

ok type me answer i can share in the chat

### 33.

look deeper into what marcus is asking and why

### 34.

Somebody has been quiet for a month. Walk me through, step by step, exactly what would have to happen for them to start getting work again.

### 35.

provide me short summary so i can understand

### 36.

what lowering their score, how do we brin their score back up?

### 37.

Find out why the four miss so many pings, because any fix that puts them back first while they keep missing could cause more unfilled callouts. Wen Li and Ravi can say whether the four answer slowly. If they do, restoring the wait comes first, then a one-time reset.

### 38.

ask

### 39.

any data in any file to these questions or mail you can find or ticket?

### 40.

ok after all this reaserch what is your summary short and to the point pls

### 41.

i need sumarry like this will you agree with this? according to my findings in the code, for someone who's gone quiet, the only way to bring your score back up is to take pings when you're asked, which means shortening your "availability" windows to only the times you can take, making sure notifications are on and the app is signed in when you're "available", and keep your matching tags up to date, be in the region where callouts frequently happen since this is currently weighted more heavily than ever.

### 42.

read few more and then i need from you based of your knowlige

### 43.

what prompt i give you i can share with team which

### 44.

how could someone who has gone quiet, bring up their score? what should they stop and start doing?

### 45.

is the code doing the mechanisne how the code is supporting this issue is the issue there what is the code not doin g

### 46.

what is missing?

### 47.

If I'd only asked what the code does, not what it doesn't do, what would I have missed? one more promped before we wrap up
