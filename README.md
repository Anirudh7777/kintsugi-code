# Kintsugi Code

**A free browser game that teaches anyone, with zero coding background, to think like a developer.**

You start your first day as a new grad at a fictional fashion brand, *Marigold & Thread*. You walk into a real-feeling office where everyone sits by role: the manager in a glass room, the engineers in a pod with the tech lead at its head, QA in their lab, DevOps by the servers, product and design nearby. Customers then arrive with real problems on a video call at your desk. You solve them by choosing an approach, commanding a small crew, teaching a robot, and surviving a sale-day rush. Along the way you learn logic and data structures through everyday situations, not a specific programming language.

This repository holds the full game: a 14-day bootcamp at Marigold & Thread, a second company (Wrenfield Community Bank), Junior to Senior careers, and 10 certification-practice Tales. The first shift, *Gift Card Counter*, takes about 15 minutes.

## Play it

Open `index.html` in a modern browser (Chrome, Edge, Firefox, Safari). No server, no install, no account.

- JavaScript runs fully offline.
- Python is available as an option and loads its runtime from the internet the first time you pick it.
- Best on a laptop with a keyboard. The office is 3D, so the browser needs WebGL (every current browser has it; if it is missing, the game skips the office walk-through).

## What is in the first shift

| Beat | What you do |
| --- | --- |
| Walk to work | Follow the guiding wind through the street to the office door; a short tour teaches the controls |
| The office | A real 3D office with glass-walled rooms, opening glass doors and a follow camera. Sam at reception greets you, Maya (manager) briefs you, then you meet Arjun (tech lead), Noor, Kai, Leo (QA), Priya (product), Zoe (design) and Ravi (DevOps). Press H for the Who's who board, V for a bird's-eye overview, the mini-map and the "Next" bar always show where to go, grab coffee to calm the team, then sit at your glowing desk: the camera zooms into your computer screen and the shift plays out inside a desktop window on that monitor |
| 1. Briefing | Maya, your manager, introduces the customer |
| 2. Live it (Standoff) | Choose an approach; see what it costs on a normal day and on a 100,000-card sale day |
| 3. Run the shop | Order your crew's steps; the crew follows them literally, so mistakes are visible and funny |
| 4. Hire the robot | Teach a robot the same job in code: pick the lines (Robot Lite), write it yourself, or let the game show you first |
| 5. Rush hour | The same logic faces 100,000 cards; slow logic means the line goes out the door |
| 6. What goes wrong? | Predict which strange customer jams the robot, then watch your robot try them all |
| 7. Review | Maya, the client and the team react; earn XP and reputation |
| Field Notebook | A personal study note for the day, with concept cards, your own mistakes and self-check questions |
| Team help | Ask Noor, Kai or Leo for help. Clear questions cost little patience; vague or repeated ones irritate them |

## Controls

| Action | Keys |
| --- | --- |
| Move | WASD or arrows (W / S also move up and down in the office) |
| Who's who board | H (or E next to it) |
| Office overview | V |
| Follow the wind | Hold Q |
| Act, talk, continue | E or Enter |
| Pick an approach | 1, 2, 3 |
| Explain the current idea | I (press again for the technical version) |
| Field Notebook | N |
| Ask a teammate | F |
| Menu, settings, controls | Esc, then C |

Accessibility: Calm mode (no timers), Reduce motion, Larger text, full keyboard play.

## Project structure

```
index.html        playable bundle (everything inlined)
build.js          bundles src/ into dist/index.html (node build.js)
src/
  index.html      page template
  styles.css      styling
  data.js         story text, glossary, tests, code templates (all Shift content)
  engine.js       state, overlays, dialogue, info cards, input
  world.js        the street and the guiding wind (canvas)
  office.js       the 3D office (three.js): rooms, glass doors, role-based seating, characters, guide trail, mini-map, interactions
  vendor/three.min.js   three.js r152 (MIT licence), bundled so the game works offline
  shift.js        shift framework, briefing and the standoff
  crew.js         the crew puzzle and its interpreter
  runner.js       runs player code safely in a Web Worker (JavaScript, Python via Pyodide)
  robot.js        hire the robot, rush hour, what goes wrong
  review.js       Day 1 review, Day 1 notebook, team help
  problems.js     bootcamp days 2-5 as data + company definitions
  problems_a..f.js  days 6-14, Wrenfield days 1-6, career tickets (data-driven missions)
  missions.js     generic mission engine for those days (brief, standoff, robot, rush, edge cases, review)
  scenarios.js    scenario engine + first incidents and Tales
  scenarios_s/h/t.js  more Marigold incidents, Wrenfield incidents, six more Tales
  hub.js          progress and levels, saving (localStorage), ticket board, multi-page Field Notebook
```

To rebuild after editing `src/`: `node build.js`, then open `dist/index.html`.

## What is playable now

- **Marigold & Thread, New grad bootcamp (14 days):** hash map, set, counting, one pass, stack, binary search, queue, recursion, tree, graph route, sliding window, database join, interval merging, and a capstone. Every day has a briefing, a standoff between approaches, a robot to teach (JavaScript or Python; Robot Lite, write-it-yourself or show-me-first), a rush-hour stress test, edge cases and a notebook entry.
- **Careers (Junior, Mid-level, Senior):** promotions at 600, 1500 and 2800 XP (or demo mode). Each level has incidents at both companies (judgement scenarios: trace and fix, design and trade-offs, lead and communicate) and one coding "career ticket" (rate limiter, LRU cache, release order).
- **Wrenfield Community Bank:** unlocks at Junior. Six coding days (running balance, two pointers, check digits, cash-machine change, longest streak, grouping) and six bank incidents (money as cents, time zones, idempotent transfers, slow statements, payday outage, core ledger migration).
- **Tales:** ten story side quests that practise ideas behind real certifications (AWS Cloud Practitioner, Solutions Architect, Developer; Azure Fundamentals; Kubernetes KCNA; Terraform; Security+; Google Cloud Digital Leader; Java SE 21; Spring), each with a Ready meter. They are practice, not official exams; exam codes shown were checked against search results on the build date and must be re-verified on the vendor sites.
- Start anywhere: the start screen lets you pick Marigold & Thread or Wrenfield and New grad, Junior, Mid-level or Senior (higher levels start at that level's XP). A "Jump to" selector and a "Demo mode" toggle on the ticket board do the same later. Progress, XP, reputation and notebook entries are saved in the browser.

Python needs internet the first time (Pyodide loads from a CDN); everything else works offline.

## Roadmap

A Java runner, more incidents per level, a second Wrenfield bootcamp half, Team lead / Staff / Principal levels, and a native-feeling mobile layout.

## Testing

`tools/verify.js` checks every coding mission (only the intended Robot Lite combination passes, the guided solution passes, the stress test finishes in time) in both languages. `tools/playmission.js` and `tools/playscen.js` play missions and scenarios end to end in a headless browser (`DIST=... node tools/playmission.js <ids>`). `test.js` plays the Day 1 flow through the office.

## Notes

- All names (Marigold & Thread, Wrenfield, characters) are fictional. Screened by web search only (see `TRADEMARK_CHECK.md`); run an official search before a commercial launch.
- Problem stories and test data are original. The underlying patterns (for example, Two Sum) are standard.
- Licensed under the MIT License (see `LICENSE`). Third-party notices are in `THIRD_PARTY_NOTICES.md`; the name screening is in `TRADEMARK_CHECK.md`.
