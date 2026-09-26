# BPLRT Full Sunday Closure — live programme

The published Gantt Studio programme for contract C801B. Anyone with the web
link sees the current plan. It **opens on the Live carousel** — `config.json`
says `"openOn": "live"` — and plays exactly what was set up in the desktop copy:
the same watched groups, the same closure, the same slide timing, because all
three travel inside `data/programme.json`. Nothing has to be set up again at
this end.

Each watched group gets a screen of its own that opens with the group itself —
what level it sits at, where it sits, its own progress against plan — and then
drills one level down: its immediate subgroups, on a rail, with an arrow into
each. Watch a subgroup instead and the same screen drills into its own
subgroups, or into its activities when it has none. The page checks for a new version on an interval you
can change from the page itself — the **refresh** box on the Live bar, beside the
play controls — and on the Live tab it takes a new version by itself, because a
wall screen has nobody standing next to it to press Reload. On every other tab it
still asks first.

## What is in here

| File | What it is |
|---|---|
| `index.html` | Gantt Studio, Revision AN. One self-contained file — no build, no dependencies, no server code. |
| `config.json` | Where the page looks for the programme, what it calls itself, and the interval it starts on. |
| `data/programme.json` | The programme itself. This is the file the Publish button rewrites. |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are. |

## Called-off work

An activity can be marked **Cancelled**. It keeps its row and its bar — greyed,
ruled through and hatched — so the record of what was planned survives, but it
counts nowhere: not in the task total, not in the percentage complete, not in the
group roll-up, not as open, overdue or unassigned. The **Cancelled** chip sits on
the status bar with the others and stacks with everything else — closure, owner,
team, location, the search box — and the Action Tracker has a matching
**Cancelled** button.

Cancelled means *not tonight* — the work could not proceed and comes back on a
later date. So it is never overdue, and it is never counted as work still owed.
What it is counted as is **cancelled scope**, and the page reports that in three
places: a **Cancelled** box in the header, giving the share of whatever the Live
chips have selected; a segment on every closure's status bar, on the wall and on
the Dashboard; and a screen of its own in the carousel — *What was called off* —
which cuts the closure three ways, booked / still to do / cancelled, and then
names each called-off activity with the group it sits in, who holds it and the
window it was meant to run in.

Two percentages, deliberately: **Complete** is measured against the work still in
the plan, because that is the number a shift manager acts on, and **Cancelled**
is measured against the scope as first planned, because that is the only
denominator a lost activity means anything against. Both say so when hovered.

## Turning it into a web page

Settings → Pages → Source: **Deploy from a branch** → Branch: **main**, folder
**/ (root)** → Save. A minute later the site is live at
`https://OWNER.github.io/REPO/`.

## Publishing an update

Open the site, press the gear beside the Gantt Studio logo, fill in the owner,
the repository and a fine-grained token with **Contents: Read and write**, then
press **Publish now**. The token is kept in that browser and nowhere else — it
never enters `data/programme.json`, so nothing in this repository can be used
to publish.

Everyone else's open tab picks the change up on its next check — within a minute
by default, or whatever their own refresh box is set to. A screen sitting on the
Live tab reloads itself; the rest are offered a **Reload** button.

## How often it checks

`config.json` carries `refreshSeconds`, which is only the starting value. On the
Live tab there is a **refresh … s** box next to the play controls: change it and
that screen checks at the new interval from then on, and remembers the setting in
that browser. Anything from 15 seconds to an hour is allowed — 15 to 30 seconds
during a closure, a few minutes the rest of the week.

## Weather boards

A weather board reads the met service from the viewer's own browser, so a
published page keeps its forecast current without anything server-side. Three
addresses need to be reachable from wherever the page is opened:

```
api.open-meteo.com
air-quality-api.open-meteo.com
geocoding-api.open-meteo.com
```

They need no key and no account. If a network blocks them the board falls back
to the last reading stored in `data/programme.json` and says how old it is.

A board reports the forecast and nothing else: the chance of rain, how much,
whether there is lightning in the window and when, the strongest gust, the lowest
visibility and the temperature range. What that means for the night's work is the
shift manager's call, not the screen's.

## A note on visibility

This repository is public, so `data/programme.json` — every activity, every
name, every time — is readable by anyone who finds it. That was a deliberate
choice: a public repository is what lets the page be opened by a link with no
sign-in. Keep anything that should not be public out of the programme file.
