# BPLRT Full Sunday Closure — live programme

The published Gantt Studio programme for contract C801B. Anyone with the web
link sees the current plan. The page checks for a new version on an interval you
can change from the page itself — the **refresh** box on the Live bar, beside the
play controls — and on the Live tab it takes a new version by itself, because a
wall screen has nobody standing next to it to press Reload. On every other tab it
still asks first.

## What is in here

| File | What it is |
|---|---|
| `index.html` | Gantt Studio, Revision AF. One self-contained file — no build, no dependencies, no server code. |
| `config.json` | Where the page looks for the programme, what it calls itself, and the interval it starts on. |
| `data/programme.json` | The programme itself. This is the file the Publish button rewrites. |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are. |

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

## A note on visibility

This repository is public, so `data/programme.json` — every activity, every
name, every time — is readable by anyone who finds it. That was a deliberate
choice: a public repository is what lets the page be opened by a link with no
sign-in. Keep anything that should not be public out of the programme file.
