# BPLRT Full Sunday Closure — live programme

The published Gantt Studio programme for contract C801B. Anyone with the web
link sees the current plan; the page checks for a new version every minute and
offers a Reload when one appears.

## What is in here

| File | What it is |
|---|---|
| `index.html` | Gantt Studio, Revision AA. One self-contained file — no build, no dependencies, no server code. |
| `config.json` | Where the page looks for the programme, what it calls itself, and how often it checks. |
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

Everyone else's open tab picks the change up within a minute.

## A note on visibility

This repository is public, so `data/programme.json` — every activity, every
name, every time — is readable by anyone who finds it. That was a deliberate
choice: a public repository is what lets the page be opened by a link with no
sign-in. Keep anything that should not be public out of the programme file.
