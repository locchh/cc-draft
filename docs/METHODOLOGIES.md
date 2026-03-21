# Software Development Methodologies

A **methodology** is simply a set of rules and practices that a team agrees to follow when building software. It answers questions like: *How do we plan? How do we divide the work? How do we know when we're done?*

Think of it like a recipe — different recipes for different situations. You wouldn't use a 5-course dinner recipe to make a quick sandwich, and you wouldn't use a sandwich recipe to run a restaurant kitchen.

---

## Overview

| Methodology | Type | Best for |
|---|---|---|
| Waterfall | Linear / Sequential | Fixed requirements, no changes expected |
| V-Model | Linear / Sequential | Safety-critical systems (medical, aerospace) |
| Scrum | Agile | Most teams, most projects |
| Kanban | Agile / Flow | Ongoing maintenance, support work |
| SAFe | Agile (scaled) | Large organizations, multiple teams |
| XP | Agile / Practices | High-quality code, fast feedback |
| TDD | Coding practice | Any project where quality matters |
| BDD | Coding practice | Teams who want specs written as plain English |
| Lean | Principles | Eliminating waste, moving fast |
| Shape Up | Product-focused | Small product teams, fixed time budgets |
| DDD | Design approach | Complex business domains |
| RUP | Iterative / Process | Enterprise projects with formal governance |

---

## 1. Waterfall

**Full name:** Waterfall Model

**The idea:** Do everything in order, one phase at a time. You cannot move to the next phase until the current one is fully complete.

```
Requirements → Design → Development → Testing → Deployment → Maintenance
```

**Analogy:** Building a house. You lay the foundation before the walls, walls before the roof. You can't go back and change the foundation once the walls are up (without enormous cost).

**When to use it:** When requirements are very clear and unlikely to change — for example, a government contract with a fixed specification.

**When NOT to use it:** When you're building a product and expect to learn and change your mind along the way (which is most software).

**Famous examples:**
- **NASA Space Shuttle software** — Mission-critical flight software built with strict sequential phases and exhaustive documentation
- **Healthcare systems** — Hospital record systems procured by governments under fixed contracts
- **Microsoft Windows (early versions)** — Windows NT and early Windows releases used Waterfall-style planning with long multi-year cycles

**Connection to AI tools:** Spec Kit borrows Waterfall's discipline — write the full spec before writing any code.

---

## 2. V-Model

**Full name:** Verification and Validation Model

**The idea:** An extension of Waterfall where each development phase is paired with a corresponding testing phase. The shape of the process looks like a "V."

```
Requirements ←————————————→ Acceptance Testing
   Design ←————————————→ System Testing
      Architecture ←————→ Integration Testing
         Coding ←————→ Unit Testing
```

**Analogy:** For every decision you make, you also write down how you'll prove it worked. Like a checklist: "I said the bridge can hold 10 tons — here's how I'll test that."

**When to use it:** Safety-critical software — medical devices, aviation systems, nuclear plants — where you must prove correctness at every level.

**Famous examples:**
- **Airbus flight control systems** — Every requirement maps directly to a test case; nothing ships without verified proof
- **Medical device firmware** (pacemakers, insulin pumps) — FDA regulations require traceability from requirement to test
- **Nuclear plant control software** — Correctness at every level is legally required, not optional

**Connection to AI tools:** Not directly used by any of the four tools, but the principle (every spec should be verifiable) is related to BDD and Spec Kit's clarification step.

---

## 3. Scrum

**Full name:** Scrum (originally a rugby term — a tight formation to restart play)

**The idea:** Break work into short cycles called **sprints** (usually 1–2 weeks). At the end of each sprint, you have working software. A small team works from a **backlog** (a prioritized list of work).

**Key roles:**
- **Product Owner (PO)** — decides what to build and in what order
- **Scrum Master (SM)** — keeps the process running smoothly, removes blockers
- **Developer** — builds the thing

**Key ceremonies:**
- **Sprint Planning** — decide what to work on this sprint
- **Daily Standup** — short daily sync (what did I do, what will I do, any blockers?)
- **Sprint Review** — show what was built
- **Retrospective** — how can we improve as a team?

**Analogy:** Instead of planning a year-long road trip in detail upfront, you plan week by week. After each week, you adjust based on what you learned.

**When to use it:** Most software teams. It's the most widely adopted agile methodology in the industry.

**Famous examples:**
- **Spotify** — Built its entire engineering culture on Scrum squads (teams), then evolved into the famous "Spotify Model"
- **Google** — Uses Scrum-based sprints across many product teams
- **Amazon** — Two-pizza teams (small enough that two pizzas can feed the team) running sprints
- **Salesforce** — Manages thousands of engineers using Scrum at scale

**Connection to AI tools:** BMAD-METHOD is directly inspired by Scrum — it has a PM (Product Manager, similar to Product Owner), a Scrum Master agent, Developer agents, and produces stories and epics (Scrum artifacts).

---

## 4. Kanban

**Full name:** Kanban (Japanese: 看板, meaning "signboard" or "billboard")

**The idea:** Visualize all your work on a board, limit how much work is in progress at once (called **WIP limits**), and let work flow continuously — no fixed sprints.

```
| To Do | In Progress (max 3) | Review | Done |
|-------|---------------------|--------|------|
| Task A | Task C             | Task E | Task F |
| Task B | Task D             |        | Task G |
```

**Analogy:** A restaurant kitchen. Food orders come in continuously. The chef doesn't say "we only cook on Tuesdays" — work flows through the kitchen as capacity allows.

**When to use it:** Support teams, bug fixing, maintenance work — anything where new tasks arrive constantly and unpredictably.

**Famous examples:**
- **Microsoft (Visual Studio Team)** — One of the earliest large-scale software Kanban adoptions, documented publicly by David Anderson
- **Zara (fashion supply chain)** — Not software, but Kanban's origin: Toyota's physical card system that Zara adapted to replenish store inventory in real time
- **GitHub** — Uses Kanban-style project boards for their own internal engineering work

**Connection to AI tools:** Not directly implemented by the four tools, but GSD's backlog management is Kanban-influenced.

---

## 5. SAFe

**Full name:** Scaled Agile Framework

**The idea:** Take Scrum/Agile and make it work for large organizations with 50–500+ people across many teams. Adds coordination layers on top of individual team Scrum.

**Key levels:**
- **Team** — individual Scrum teams working in sprints
- **Program** — multiple teams synchronized into a longer cycle called a **Program Increment (PI)**, typically 10 weeks
- **Portfolio** — strategic alignment across all programs

**Analogy:** Scrum is a single restaurant kitchen. SAFe is a restaurant chain — each location runs its own kitchen, but they're all aligned on the same menu and brand standards.

**When to use it:** Large enterprises where many teams need to coordinate and deliver together.

**Famous examples:**
- **Lego** — Used SAFe to coordinate 30+ teams building digital products simultaneously
- **Cisco** — Adopted SAFe across its engineering org to align hundreds of teams
- **US Air Force** — Adopted SAFe for large government software programs
- **John Deere** — Uses SAFe to coordinate software development across hardware and software teams

**Connection to AI tools:** BMAD's scale-adaptive intelligence and modular ecosystem were designed with SAFe-like complexity in mind.

---

## 6. XP

**Full name:** Extreme Programming

**The idea:** Take good coding practices and turn them up to the extreme. XP is defined by a set of specific technical practices:

- **Pair programming** — two developers share one keyboard; one writes, one reviews in real time
- **Test-Driven Development (TDD)** — write tests before writing code (see section 7)
- **Continuous Integration (CI)** — merge and test code multiple times per day
- **Small releases** — ship frequently, in tiny increments
- **Refactoring** — continuously improve code quality as you go
- **Simple design** — always use the simplest design that works

**Analogy:** Instead of waiting until the end of a long road trip to check if you're going the right way, you check the map every few minutes.

**When to use it:** Teams that care deeply about code quality and want very fast feedback loops.

**Famous examples:**
- **Chrysler Comprehensive Compensation System (C3)** — The project where Kent Beck invented XP in 1996; it's the original XP project
- **Facebook (early years)** — "Move fast and break things" era used many XP practices: continuous integration, small releases, refactoring
- **Pivotal Labs** — The consulting firm famous for practicing strict XP (pair programming all day, every day) with client teams

**Connection to AI tools:** GSD's philosophy is XP-influenced — small, clean contexts, frequent execution, and continuous refinement.

---

## 7. TDD

**Full name:** Test-Driven Development

**The idea:** Write a failing test first, then write just enough code to make it pass, then clean up the code. Repeat.

```
Red → Green → Refactor
(write failing test) → (make it pass) → (clean it up)
```

**Analogy:** Imagine writing the exam questions before studying. You study specifically to pass those questions — and you know exactly when you're done.

**When to use it:** Any project where correctness matters. Especially useful when requirements are clear and stable.

**Famous examples:**
- **Ruby on Rails** — David Heinemeier Hansson (DHH) built Rails with TDD as a core practice; the Rails community made TDD mainstream in web development
- **Django** — Python web framework, built and maintained with TDD throughout
- **JUnit / RSpec** — The testing frameworks themselves were built TDD-first and became industry standards

**Connection to AI tools:** TDD is a coding *practice*, not a full workflow, but it's compatible with all four tools. Spec Kit's task files can include test scenarios.

---

## 8. BDD

**Full name:** Behavior-Driven Development

**The idea:** An extension of TDD where tests are written in plain English using a specific format called **Given-When-Then**, making them readable by both developers and non-technical stakeholders.

```
Given: a user is logged in
When: they click "Delete Account"
Then: their account is removed and they receive a confirmation email
```

**Analogy:** TDD asks "does the code work?" BDD asks "does the code do what the user actually needs?"

**Common tool:** Gherkin (the language), used with frameworks like Cucumber or Behave.

**When to use it:** When you want your specifications and your tests to be the same document — one that both business people and developers can read and agree on.

**Famous examples:**
- **GOV.UK** — The UK government's digital services platform uses BDD extensively so non-technical policy teams can read and validate test scenarios
- **Cucumber (the tool itself)** — Built by Aslak Hellesøy specifically to enable BDD; now used by thousands of companies including Typeform, Badoo, and others
- **Salesforce** — Uses BDD for its platform acceptance testing to align product, QA, and engineering

**Connection to AI tools:** BDD's "spec as plain English" idea is the philosophical ancestor of Spec Kit's spec-first approach.

---

## 9. Lean Software Development

**Full name:** Lean Software Development (adapted from Lean Manufacturing / Toyota Production System)

**The idea:** Seven principles borrowed from Toyota's manufacturing process, applied to software:

1. **Eliminate waste** — don't build features nobody needs
2. **Amplify learning** — get feedback early and often
3. **Decide as late as possible** — defer irreversible decisions
4. **Deliver as fast as possible** — speed reduces risk
5. **Empower the team** — decisions should be made by those closest to the work
6. **Build integrity in** — quality is not a phase; it's built in from the start
7. **See the whole** — optimize the whole system, not just individual parts

**Analogy:** Toyota noticed that the biggest waste in car manufacturing wasn't slow workers — it was waiting, inventory, and defects. The same is true in software: most time is wasted waiting for approvals, building unused features, or fixing bugs that could have been prevented.

**When to use it:** Its principles are universal. Most modern agile approaches (Scrum, Kanban, XP) have Lean at their core.

**Famous examples:**
- **Toyota Production System** — The origin. Toyota eliminated waste so effectively it became the most efficient car manufacturer in the world
- **Spotify** — Explicitly applies Lean principles: small autonomous squads, eliminate handoffs, continuous deployment
- **Netflix** — Lean thinking underpins their "highly aligned, loosely coupled" culture; minimize process, maximize flow
- **Eric Ries' Lean Startup** — Applied Lean to startups: build→measure→learn loop; products like Dropbox and Airbnb used it in their early days

**Connection to AI tools:** GSD is the most Lean-influenced of the four — its entire design is about eliminating waste (context rot) and delivering in small, clean increments.

---

## 10. Shape Up

**Full name:** Shape Up (created by Basecamp, described in their free book *Shape Up* by Ryan Singer)

**The idea:** Work in **6-week cycles** with a structured process:

1. **Shape** — a small senior group defines the *problem and rough solution* (not detailed specs) before any team works on it
2. **Bet** — leadership explicitly *bets* on which shaped work to fund this cycle (no backlog piling up)
3. **Build** — small teams (1–2 people) have full autonomy to figure out the implementation within 6 weeks
4. **Cool-down** — 2 weeks after each cycle for bug fixes, experiments, and rest

**Key difference from Scrum:** There is **no backlog**. Ideas that don't get bet on in a cycle are discarded, not queued. "If it's not worth betting on now, it probably never was."

**Analogy:** Instead of a restaurant with an ever-growing order queue, the chef decides at the start of each week exactly what dishes will be made — and only those. Anything not on the menu this week simply isn't served.

**When to use it:** Small, autonomous product teams that want to avoid the chaos of a never-ending backlog and want meaningful, focused work cycles.

**Famous examples:**
- **Basecamp** — Shape Up was invented here and is still how the Basecamp and Hey products are built today
- **37signals** — Same company as Basecamp; all products (HEY email, Basecamp) use Shape Up
- **Podia** — Online course platform that publicly adopted Shape Up and documented their transition from Scrum

**Connection to AI tools:** The "shaping" concept (define the problem and constraints before the team touches it) is similar to how Spec Kit's `constitution` + `specify` steps work.

---

## 11. DDD

**Full name:** Domain-Driven Design (introduced by Eric Evans in his 2003 book *Domain-Driven Design: Tackling Complexity in the Heart of Software*)

**The idea:** The most important thing in a complex software system is understanding the *domain* — the real-world problem space you're working in (e.g., banking, healthcare, e-commerce). Your code should reflect that domain using the same language that domain experts use.

**Key concepts:**
- **Ubiquitous Language** — developers and business experts use the *exact same words* for things. No translation layer.
- **Bounded Context** — a boundary around a part of the system where a specific model applies. (e.g., "Order" means something different in the Shipping context vs. the Billing context.)
- **Entities and Value Objects** — ways of modeling real-world things in code
- **Aggregates** — clusters of objects that are treated as a single unit

**Analogy:** A doctor and a software developer working on a hospital system should both call the same thing a "Patient Admission" — not the doctor calling it that while the developer calls it a `UserCheckIn` object.

**When to use it:** Complex business domains where the logic is intricate and the language precision matters. Overkill for simple CRUD apps.

**Famous examples:**
- **Uber** — Uses DDD with bounded contexts separating Rides, Payments, Driver Management, and Notifications — each with their own domain models
- **SoundCloud** — Migrated from a monolith to microservices using DDD bounded contexts as the boundaries
- **LinkedIn** — Uses DDD to model complex social graph, job matching, and feed ranking domains separately

**Connection to AI tools:** Agent OS is DDD-influenced — its core idea is that agents must first *understand the standards and patterns of your codebase* (your domain) before writing code. Without that, they produce inconsistent code.

---

## 12. RUP

**Full name:** Rational Unified Process (developed by Rational Software, acquired by IBM)

**The idea:** An iterative software development process that is more structured and document-heavy than Scrum, but more flexible than Waterfall. It defines four phases:

1. **Inception** — understand the scope, feasibility, and risks
2. **Elaboration** — define the architecture and resolve major risks
3. **Construction** — build the system iteratively
4. **Transition** — deploy to users, gather feedback, finalize

Unlike Waterfall, you iterate within each phase. Unlike Scrum, you still produce heavy documentation and formal artifacts.

**Analogy:** Building a skyscraper. You first confirm the project makes sense (Inception), then design the structural frame (Elaboration), then fill in all the floors (Construction), then hand over the keys (Transition).

**When to use it:** Large enterprise or government projects where formal documentation, traceability, and governance are required.

**Famous examples:**
- **IBM WebSphere** — Developed internally at IBM using RUP; IBM was both the creator of the process and the primary user
- **Siemens enterprise software** — Large industrial software systems built under RUP for formal traceability
- **US Department of Defense projects** — Many DoD software contracts in the 2000s mandated RUP-compliant processes

**Connection to AI tools:** BMAD's multi-phase structure (brainstorm → PRD → architecture → stories → dev loop) loosely mirrors RUP's four phases, but executed with AI agents instead of human teams.

---

## How These Methodologies Relate to the Four AI Tools

The four tools in this project don't invent new methodologies — they *apply* existing ones to AI-assisted development:

| AI Tool | Inspired by | Why |
|---|---|---|
| **GSD** | Lean + XP | Eliminate waste (context rot), small clean increments, fast execution |
| **BMAD-METHOD** | Scrum + SAFe | Specialist agent roles mirror Scrum team roles; scale-adaptive like SAFe |
| **Spec Kit** | Waterfall spec discipline + BDD | Write the full spec before coding; specs are human-readable like BDD scenarios |
| **Agent OS** | DDD | Agents must know your domain (standards, patterns) before they can write good code |

The key insight: **methodology matured over decades of human teams learning painful lessons**. AI tools are now encoding those lessons into automated workflows so you get the benefits without needing a large team or a formal process certification.

---

## Glossary

| Term | Full form | Plain meaning |
|---|---|---|
| BDD | Behavior-Driven Development | Write tests as plain English user stories |
| CI | Continuous Integration | Merge and test code many times per day |
| DDD | Domain-Driven Design | Model your code around the real-world business domain |
| PI | Program Increment | A ~10-week synchronized cycle across multiple Scrum teams (SAFe) |
| PM | Product Manager / Product Owner | The person who decides what gets built |
| PRD | Product Requirements Document | A document describing what the product should do |
| RUP | Rational Unified Process | IBM's structured iterative development process |
| SAFe | Scaled Agile Framework | Agile practices scaled up for large organizations |
| SDD | Spec-Driven Development | Write the specification before writing any code |
| SM | Scrum Master | The person who keeps the Scrum process running |
| TDD | Test-Driven Development | Write tests before writing code |
| WIP | Work In Progress | Tasks currently being worked on (Kanban limits this number) |
| XP | Extreme Programming | Agile methodology focused on rigorous coding practices |
