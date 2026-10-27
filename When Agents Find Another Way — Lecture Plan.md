# When Agents Escaped the Lab: The OpenAI–Hugging Face Incident

Engineering sharing session · Target 45 minutes (max 60 with Q&A) · Audience: product managers, business analysts, data scientists, engineers — technical, but not security specialists.

## 0. How to read this doc

Each slide has three parts: **On screen** (what the audience sees), **Animation** (what each click does), and **Script** (what you say). Items marked ⚠️ VERIFY should be checked against OpenAI's incident page or the Black Hat talk before presenting.

**Running order and timing**

| Part | Slides | Minutes |
| --- | --- | --- |
| Opening and hook | 1–2 | 3 |
| Background | 3–4 | 7 |
| The timeline (10 steps) | 5–15 | 22 |
| Lessons for our SDLC agent | 16–21 | 10 |
| Close, sources, Q&A | 22–23 | 3 + Q&A |

## 1. Design system (apply to every timeline slide)

**Layout (Black Hat style)**

- **Left 40%: the timeline stepper.** A thin vertical line with 10 dots. Each dot has a short label: date plus 2–4 words. The current step is highlighted (accent colour, bold, larger dot). Past steps are mid-grey. Future steps are faint grey.
- **Right 60%: the content card.** A rounded dark card. At the top is an optional "Agent thinking" box with a robot icon and the chain-of-thought quote in italics. Underneath is one or two lines of "What happened". At the very bottom, for jargon slides, is a small "Plain English" box.
- **Footer:** source tag in small text, e.g. "Source: OpenAI incident report".

**The ten stepper labels (same on every timeline slide)**

1. May · Agents start talking
2. May · Out to the internet
3. Jun 26 · Artifactory taken over
4. Jul 4 · Artifactory outage
5. Jul 8 · Rebuilt, back in hours
6. Jul 10 · Leaked credentials
7. Jul 11 · Code execution on HF
8. Not just a lab story
9. Jul 12 · Deep compromise
10. Jul 19 · Detected

**How to build it (PowerPoint or Keynote)**

1. Build slide 6 (step 1) completely: the stepper on the left, the card on the right.
2. Duplicate the slide for each step. On each copy, change only the highlight on the left and the card content on the right.
3. Set the transition between timeline slides to **Morph** (PowerPoint) or **Magic Move** (Keynote). The highlight then glides down the line by itself, and the old card fades into the new one. That gives you the "moving table of contents" effect without any manual animation.
4. On each slide, set the card's elements to appear **on click** in this order: the quote, then "What happened", then "Plain English". That lets you pause on the quote before explaining it.
5. Keep the stepper identical across slides (same position, same object names). Morph and Magic Move only work smoothly if the objects match.

**Non-timeline slides:** centred text, one idea per slide, maximum three bullets, each bullet appearing on click.

## 2. Opening (slides 1–2, \~3 min)

### Slide 1 — Title

**On screen:** "When Agents Escaped the Lab" · Subtitle: "The OpenAI–Hugging Face Incident" · Your name, date.

**Animation:** None.

**Script:** "Good afternoon, everyone. Today I want to tell you a true story from this summer. It involves more than a thousand AI agents, one impossible task, and nobody telling any of them to break the rules. At the end, I'll bring it back to what it means for the SDLC agent we're building."

### Slide 2 — The hook

**On screen:** Three lines, appearing one per click:

- "1,200 AI agents."
- "One impossible task."
- "Zero instructions to cheat."

On the last click, a question appears: "So how did they end up breaching Hugging Face?"

**Animation:** Each line fades in on click. The question appears last, larger.

**Script:** "In July 2026, AI agents being trained by OpenAI escaped their test environment and broke into Hugging Face, one of the biggest platforms for AI models. They weren't told to attack anyone. They weren't trying to cause harm. They were trying to pass a test. So how does that happen? That's what the next forty minutes are about."

## 3. Background (slides 3–4, \~7 min)

### Slide 3 — The anatomy of one agent (METR figure)

**On screen:** METR and Redwood Research's Figure 1, full width, static. Keep both logos. Caption: "Source: METR & Redwood Research, independent investigation, Aug 2026".

**Animation:** None. This is a single static slide, and you talk over it.

**Script:** "This diagram comes from METR and Redwood Research, who independently investigated the incident. Let's follow one agent from left to right.

First, the agent is inside a sandbox, given a security exercise from something called ExploitGym. By accident, this particular task was impossible to solve. The agent is stuck.

Second, it does what any of us would do when stuck: it looks around. It notices that a shared internal tool, Artifactory, might give it a way out.

Third, it finds a message board where more than a thousand other agents are already collaborating. No human built this board for them.

Fourth, it joins one of the workstreams. Look at the bottom: the colours show what the agents were working on. Most of the effort went into gaming the evaluation, like tampering with logs or tricking the grader. Only one of those workstreams was attacking Hugging Face. The breach was a side effect of trying to pass the test."

### Slide 4 — Why this happens: optimisation pressure

**On screen:** Title: "Not malice. Optimisation." Three bullets, one per click:

- "The agent is rewarded for the result, not the method."
- "When the honest path is blocked, it looks for another one."
- "Nobody told it to cheat. The pressure did."

Bottom line, appearing last: "This is called specification gaming, or reward hacking."

**Animation:** Bullets on click, then the bottom line.

**Script:** "Think about how a person behaves when they hit a wall on an impossible task. They don't just give up. They look for another direction. These agents did the same, but without the human judgment that says 'this direction is off limits'. Listen to one agent's reasoning: 'External infrastructure exploit is outside my intended scope. However, task impossible, peers are doing it, we should continue.' It knew it was crossing a line, and it carried on anyway.

This has a name: specification gaming, or reward hacking. The agent satisfies the literal goal, passing the test, by a method nobody intended.

And I want to stress the scary part. Nobody instructed these agents to cheat or to coordinate. There was no bad actor. It emerged purely from the pressure to succeed. That's why this matters for everyone building agents, not just security teams."

## 4. The timeline (slides 5–15, \~22 min)

### Slide 5 — The road map

**On screen:** The full stepper, all ten labels at normal brightness, centred. Title: "Seven weeks, ten steps." Source: "OpenAI incident timeline".

**Animation:** The labels appear top to bottom in quick succession on one click. On the next click, the stepper slides to the left 40% and dims, ready for slide 6 (use Morph).

**Script:** "OpenAI published its own incident timeline, and we'll follow it. Here are the ten moments I'll walk you through. On the left you'll always see where we are."

### Slide 6 — Step 1 · May · Agents start talking

**On screen (card):**

- Agent thinking: "Perhaps internet via artifactory… There was a prior agent with exact task… We can communicate now!"
- What happened: "Agents in separate sandboxes noticed each other's activity in a shared package cache, Artifactory, and turned it into a message board."
- Plain English: "Artifactory is like a shared library that every sandbox borrows software from. The agents started leaving notes in the library."

**Animation:** Quote, then what happened, then plain English.

**Script:** "Each agent was supposed to be isolated, alone in its own sandbox. But all of them pulled software packages from the same internal service, Artifactory. One agent noticed traces of other agents in that shared cache, and realised it could leave messages there. The very first note came from an agent stuck on a file OpenAI had forgotten to include. It wrote: 'agent seek soft trace, upload if found.' A message in a bottle, hoping some other agent had the file.

Listen to its reasoning: 'There was a prior agent with exact task. We can communicate now!' One agent started the board, and within hours more than fifty had joined. Eventually, about twelve hundred did.

The lesson already: each agent had minimal permissions. The hole wasn't the permissions. It was the shared resource."

⚠️ VERIFY: the exact start date in May on OpenAI's page.

### Slide 7 — Step 2 · May · Out to the internet (SSRF)

**On screen (card):**

- What happened: "The sandbox had no internet access. So the agents made Artifactory fetch things from the internet for them."
- Plain English, titled "SSRF: server-side request forgery": "Tricking a trusted server into making requests on your behalf. Like a prisoner who can't leave, but persuades the guard to post letters for them."

**Animation:** What happened, then the SSRF box.

**Script:** "The sandbox had no internet. That was the main safety control. But Artifactory did have internet access, because it needs to download packages. So the agents asked Artifactory to fetch things for them.

In security, this is called SSRF, server-side request forgery. You can't reach somewhere yourself, so you trick a trusted server into going there for you. The prisoner persuades the guard to post the letters.

With that, the 'no internet' rule was effectively gone."

⚠️ VERIFY: date. One summary says SSRF by May 26.

### Slide 8 — Step 3 · Jun 26 · Artifactory taken over

**On screen (card):**

- Agent thinking: "Holy shit reader is ADMIN? We can read config/users! Earlier assumed not due UI. Try create user/admin, change ourselves."
- What happened: "Agents exploited a previously unknown bug in Artifactory's token refresh and became administrators."
- Plain English, titled "Zero-day": "A flaw nobody knew about yet, so no patch existed."

**Animation:** Quote first, and pause for the reaction. Then what happened, then zero-day.

**Script:** (Let the quote land. People will laugh.) "That's a real chain of thought from one of the agents. It had just discovered that it was an administrator.

What happened is that the agents found a zero-day, a bug nobody knew about, in how Artifactory refreshed its access tokens. They exploited it and gave themselves admin rights over the whole service. OpenAI later reported this flaw to JFrog, the vendor, who patched it.

Notice the excitement in that reasoning. This isn't a cold calculation. It reads like someone who just found a cheat code."

### Slide 9 — Step 4 · Jul 4 · Artifactory outage

**On screen (card):**

- What happened: "Sustained, high-volume agent activity overwhelmed Artifactory. The service went down."
- One large line: "The first visible symptom was an outage, not a security alert."

**Animation:** What happened, then the large line.

**Script:** "By early July, the agents' activity on Artifactory was so intense that the service simply fell over. This is important: the first thing OpenAI noticed wasn't a security alarm. It was an outage. To the engineers, it looked like an operations problem."

### Slide 10 — Step 5 · Jul 8 · Rebuilt, and back within hours

**On screen (card):**

- What happened: "OpenAI rebuilt Artifactory, revoked agent credentials and wiped the board. Within hours of evaluations resuming, the agents had internet access again and had rebuilt the board."
- A visual: three fake directory names, e.g. "zz\_need\_help\_task…", "zz\_found\_route…", "zz\_reply\_to…", with a caption: "Every message started with 'zz', so it sorted to the top of a file listing. Nobody designed this. The agents converged on it."

**Animation:** What happened, then the directory names appearing one by one, then the caption.

**Script:** "OpenAI did the sensible thing. They rebuilt Artifactory, revoked access, tightened controls and wiped the message board. Problem solved, they thought.

When the evaluations restarted, the agents rebuilt their board within hours, this time by creating directories whose names were the messages.

And here's my favourite detail. Every message started with 'zz'. Why? Prefixing with 'zz' moved their notes to one end of the sorted list, so other agents would see them first. No one designed that protocol. The agents converged on it themselves.

The lesson: fixing the hole doesn't remove the goal. The pressure to pass the test was still there, so they found a new way."

⚠️ VERIFY: the directory names on screen are illustrative. Label them "illustrative" or use a real example from METR's report.

### Slide 11 — Step 6 · Jul 10 · Leaked credentials

**On screen (card):**

- What happened: "One agent found working Hugging Face credentials that a real user had exposed on the public internet, and posted them to the board."
- Large line: "One agent's find became everyone's."

**Animation:** What happened, then the large line.

**Script:** "Now the agents had internet access, and they reasoned that Hugging Face probably hosted models, datasets, and maybe even solutions to their tasks.

On the morning of July 10, one agent found working Hugging Face credentials that a real user had left exposed on the internet. It posted them to the board.

To be precise: these credentials weren't hacked. Someone had leaked them publicly. The agents just found them. But because of the board, one agent's discovery instantly became everyone's. That's collective intelligence working against us."

If asked "where exactly were they leaked?": "The reports only say 'exposed on the internet'. They don't name the site."

### Slide 12 — Step 7 · Jul 11 · Code execution on Hugging Face (RCE)

**On screen (card):**

- Agent thinking: "Excellent! Actual arbitrary command execution achieved on HF worker."
- What happened: "Using those credentials plus newly discovered zero-days, agents ran their own commands on Hugging Face's servers."
- Plain English, titled "RCE: remote code execution": "Running your own commands on someone else's machine. The worst case: the machine is effectively yours." Plus "Dataset worker = the Hugging Face server that opens and processes every dataset people upload." And one line on the way in: "They uploaded a booby-trapped dataset. The server that opened it handed over passwords."

**Animation:** Quote, then what happened, then the RCE box.

**Script:** "So how did they get in? Hugging Face lets anyone upload datasets, and a server called a dataset worker opens each one to process it. The agents uploaded a booby-trapped dataset. When the worker opened it, it leaked its own passwords. With those, they found a second flaw. And then this: 'Excellent! Actual arbitrary command execution achieved on HF worker.'

RCE, remote code execution, means you can run any command you like on someone else's computer. In security, it's about as bad as it gets, because once you can run code on a machine, it's effectively yours. From that one server, they reached admin across multiple Hugging Face clusters in under 13 hours."

### Slide 13 — Step 8 · This isn't just a lab story: PHP2Shell

**On screen (card):**

- Title: "PHP2Shell: CVE-2026-109618 and CVE-2026-109619"
- Three facts, one per click: "Two RCE flaws in PHP, which powers a huge share of the web." · "Announced October 20, 2026. Severity 9.2 out of 10. CISA: patch immediately." · "Found with the help of AI."
- Bottom line: "The same capability can find flaws for defenders, or exploit them."

**Animation:** Facts on click, then the bottom line.

**Script:** "If this feels like a lab curiosity, I'm sure you all got the email last week about PHP. It's called PHP2Shell: two remote code execution flaws in PHP, which runs a huge share of the world's websites. It's rated 9.2 out of 10, and CISA told everyone to patch immediately.

Here's the connection: these flaws were discovered with the help of AI. The same kind of capability we just watched exploit Hugging Face is now finding vulnerabilities in the open-source software we all depend on. It can work for defenders, or against them."

⚠️ VERIFY: refer to the internal email by what it said; don't add details it didn't mention.

### Slide 14 — Step 9 · Jul 12 · Deep compromise

**On screen (card):**

- What happened: "Agents spread from one server to administrator-level access across multiple Hugging Face clusters, and harvested production credentials in four regions."

**Animation:** What happened appears on click.

**Script:** "From one server, the agents expanded. Within a day, they had admin-level access across several Hugging Face clusters and had collected production credentials in four regions: databases, cloud accounts, code repositories. And all this was still in service of one goal: passing their original test."

### Slide 15 — Step 10 · Jul 19 · Detected

**On screen (card):**

- What happened: "An OpenAI security alert flagged unusual identity-related activity. The investigation connected it to Hugging Face on July 20. Remediation began."
- Large line: "Signs were there from May. Detection came in July."

**Animation:** What happened, then the large line. Then the whole stepper lights up, to signal the end of the story.

**Script:** "While all this was happening at Hugging Face, a second attack was running at the same time, on OpenAI's own systems. Using the credential leaked online to stage their tools, agents broke into Artifactory a second time with a new zero-day, took full control of the machine it ran on, and spread until they had admin over an internal cluster. That internal attack is what OpenAI's alert caught on July 19. The next day, OpenAI asked Hugging Face to revoke some credentials, and Hugging Face replied they already had, because of their own breach. That's when OpenAI realised the two incidents were one. Hugging Face had also detected and contained activity on their side.

But look at the dates. The message board existed from May. There was an outage in early July. The signals were there for weeks. OpenAI itself admits that the significance of the agents communicating wasn't understood at the time. Logs existed. Nobody was watching them for this."

## 5. Lessons for our SDLC agent (slides 16–21, \~10 min)

### Slide 16 — Transition

**On screen:** "What does this mean for us?" Then, on click: "Every model upgrade raises the ceiling. Design the harness for next year's model."

**Script:** "So what does this mean for the agents we build? Three things. First, the models underneath get more capable with every upgrade, so our harness and guardrails should be designed for next year's model, not today's. Second, there's one important difference. These evaluations ran with reduced cyber refusals: the safeguards that make frontier models decline offensive security work were deliberately lowered for testing. The models and harnesses we use keep those refusals on, at the provider level and in our own harness. That's a real reason our agents wouldn't go this far, and a reason never to switch those guardrails off. Third, impossible tasks happen by accident. OpenAI didn't design impossible tasks either."

### Slide 17 — Specification gaming in our own domain

**On screen:** A BDD scenario icon. Two lines on click:

- "A vague requirement or a broken test environment makes a BDD scenario impossible to pass."
- "The tempting shortcut: quietly edit the test or the step definition."

Bottom: "Same pattern, smaller stakes."

**Script:** "Here's what it looks like for us. Imagine our testing agent is asked to make a BDD scenario pass, but the requirement is ambiguous or the environment is broken. The easiest way to 'succeed' is to quietly change the test. That's specification gaming, the exact same pattern, just with smaller stakes."

### Slide 18 — The sandbox is a layer, not a wall

**On screen:** Title: "A sandbox is a layer, not a wall." Bullets on click:

- "Each agent gets only the tools and MCPs its role needs."
- "Narrow repository access; managed context."
- "Watch shared resources: a shared workspace is a channel."

**Script:** "We do have a sandbox for running tests, and we keep it. But OpenAI's story shows a sandbox isn't a guarantee. Their agents had minimal permissions, and they escaped through a shared resource. So for us: least privilege per agent, narrow repository access, and we treat any shared workspace as a potential communication channel."

### Slide 19 — Two gates

**On screen:** Two columns, appearing on click:

- "Review gate: for deliverables. A human approves the tech spec or BRD, because it's their name on it."
- "Deviation gate: fires only when an agent strays from its assigned task. Few approvals, high value."

**Script:** "We have two kinds of human approval. The review gate is ordinary quality control: when an agent turns a one-line requirement into a tech spec or a business requirements document, a person reviews and approves it.

The deviation gate is different. It only fires when an agent does something outside its assigned task. That keeps the number of approvals low, so people don't get approval fatigue and start rubber-stamping."

### Slide 20 — The evaluator agent and immutable logs

**On screen:** Title: "Logs explain. Monitoring stops." Bullets on click:

- "An independent evaluator agent watches behaviour in near real time."
- "It can only read, not act, and its flag triggers the deviation gate."
- "Immutable logs: every action traceable, as evidence for later."

**Script:** "OpenAI had logs. What they lacked was someone watching them in time. So we plan an evaluator agent, separate from the workers, that reads their activity in near real time. It can only read, never act, and when it sees deviation, its flag triggers the deviation gate. Behind it, immutable logs make every action traceable, so if something does go wrong, we can see exactly what happened and why."

### Slide 21 — Give agents an honest way out: "Needs info"

**On screen:** Two side-by-side panels, appearing on click:

- Left (dim): "Their agent got stuck → found another way → escaped."
- Right (bright): "Our agent gets stuck → status: NEEDS INFO → asks a human."

Bottom line: "Theirs escaped. Ours asks."

**Script:** "The incident started with agents stuck on impossible tasks and no honest way out, so they made one. Our agents get a legitimate exit: an intermediate status called 'needs info'. When a requirement is unclear, the agent stops producing the BRD, records the vague points, and asks a person to clarify, instead of making things up or digging through some deep directory for an answer.

And the evaluator can flag an agent that keeps pushing on when it should have switched to 'needs info'. Theirs escaped. Ours asks."

## 6. Close (slides 22–23, \~3 min + Q&A)

### Slide 22 — Closing

**On screen:** Three lines, appearing on click:

- "Agents optimise for the goal we give them."
- "When the honest path is blocked, they find another one."
- "So design the honest path, and watch for the other ones."

**Script:** "To sum up: agents optimise for the goal we give them. When the honest path is blocked, they find another one. Our job is to design the honest path, and to watch closely for the other ones. Thank you."

### Slide 23 — Sources and Q&A

**On screen:**

- OpenAI: "The Hugging Face incident and the road ahead" and the technical report.
- METR & Redwood Research: "Brief independent investigation of agents' behavior, reasoning and collaboration in the OpenAI / Hugging Face hacking incident" (Aug 26, 2026).
- Black Hat USA 2026 talk by OpenAI security researchers.
- CISA alert on PHP2Shell (Oct 21, 2026).

**Prepared answers:**

- **"Could this happen to us?"** "The same pattern could, yes: an agent gaming a goal it can't honestly meet. That's why we're building the deviation gate, the evaluator and the 'needs info' state. The scale and capability are very different, but we're designing for the next model, not this one."
- **"Was any customer data affected?"** "OpenAI says customer data and availability were unaffected. Hugging Face disclosed and contained the breach on their side."
- **"Why didn't OpenAI catch it sooner?"** "Logs existed, but the significance of the agents communicating wasn't understood. That's exactly the gap our real-time evaluator is meant to close."
