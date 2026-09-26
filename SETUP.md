# Gantt Studio — Revision AN.online
## Hosting it on GitHub, and publishing straight from the page

Everything here is done once. After that, updating the programme everyone sees
is one button.

Throughout, replace **`OWNER`** with your GitHub username or organisation, and
**`REPO`** with the repository name you choose. `bplrt-fsc` is a good name.

---

## Part 1 · Put the repository up (about ten minutes)

### 1. Make the repository

Go to <https://github.com/new>.

| Field | What to put |
|---|---|
| Repository name | `bplrt-fsc` |
| Description | BPLRT Full Sunday Closure — live programme |
| Visibility | **Public** |
| Initialise with a README | leave unticked |

Press **Create repository**.

> **Why public.** A public repository is what lets the page open from a link
> with no GitHub sign-in. It also means `data/programme.json` — every activity,
> every name, every time — can be read by anyone who finds the address. You
> accepted that trade earlier in the project; it is worth saying again here, and
> worth keeping anything genuinely confidential out of the programme file.

### 2. Upload the four files

You have them in **`BPLRT_FSC_github_repo.zip`**. Unzip it somewhere — you
should see:

```
index.html          ← Gantt Studio, Revision AN
config.json         ← what the page reads and how often
data/programme.json ← the programme itself
.nojekyll           ← tells GitHub Pages to serve files as they are
README.md           ← this repository, explained
SETUP.md            ← this guide
```

On the empty repository page, click **uploading an existing file**. Drag in
everything *except* the `data` folder, then commit. Click **Add file → Upload
files** again and drag the whole `data` folder in, then commit again.

> If `.nojekyll` does not appear in the file picker, your computer is hiding
> dotfiles. On a Mac press <kbd>⌘</kbd><kbd>⇧</kbd><kbd>.</kbd> in the Finder to
> show them. It is not essential — the site works without it — but it stops
> GitHub Pages trying to be clever with the files.

### 3. Switch the web page on

In the repository: **Settings → Pages**.

- **Source**: Deploy from a branch
- **Branch**: `main`, folder `/ (root)`
- **Save**

Wait a minute, then open:

```
https://OWNER.github.io/REPO/
```

You should see the programme, with a green bar along the top saying **published
…** and **checked just now**. That bar is the page telling you it is live and
when it last looked for a newer version.

That address is what you send to everyone. They need no account, no token and
no explanation — the page opens read-only for them and keeps itself current.

---

## Part 2 · Let the page publish (about five minutes)

### 4. Make a token

A token is what proves to GitHub that a commit is really from you. Make one
that can do exactly one thing — write files in this one repository — and
nothing else.

Go to **<https://github.com/settings/personal-access-tokens/new>**
(Settings → Developer settings → Personal access tokens → **Fine-grained
tokens** → Generate new token).

| Field | What to put |
|---|---|
| Token name | `Gantt Studio publish` |
| Expiration | 90 days, or a custom date past the last closure |
| Resource owner | your own account |
| Repository access | **Only select repositories** → pick `REPO` |
| Permissions → Repository permissions → **Contents** | **Read and write** |

Leave every other permission alone. Press **Generate token** and copy the
string that appears — it starts `github_pat_…` and GitHub will never show it
to you again.

> **Why fine-grained rather than classic.** A classic token with the `repo`
> scope can write to every repository you can reach. This one can write files in
> one repository and do nothing else, and it expires by itself.

### 5. Connect the page to the repository

Open your site, `https://OWNER.github.io/REPO/`.

Press the small **gear** beside the Gantt Studio logo, top left. Fill in:

| Field | Value |
|---|---|
| Owner | `OWNER` |
| Repository | `REPO` |
| Branch | `main` |
| File in the repository | `data/programme.json` |
| Access token | paste the `github_pat_…` string |

Press **Check connection**. It should turn green and say **Connected**, naming
the account the token belongs to.

Now **reload the page**. This time it opens *unlocked* — the header reads
`REVISION AN · PUBLISHING`, the toolbar is live, and the green bar has a
**Publish** button on it. Everyone else still gets the read-only page, because
the unlocking is done by the token in your browser, not by anything in the
repository.

> **Where the token lives.** In that browser, on that computer, under its own
> key. It is never written into `data/programme.json`, never committed, never
> put in a share link and never in an export. Nobody opening the public page can
> publish with it. If you use a second computer, do step 5 again there. To take
> publishing away from a machine, press **Forget the token** on it — or, if the
> laptop is lost, delete the token on GitHub and every copy of it dies at once.

### 6. Make updates appear in seconds instead of a minute

GitHub Pages rebuilds the site after each commit, which takes a little while.
Reading the programme file straight from GitHub's raw host skips that wait.

In the gear dialog press **Copy config.json**. It writes out the right settings
for your repository, with the raw address already filled in:

```json
{
  "dataUrl": "https://raw.githubusercontent.com/OWNER/REPO/main/data/programme.json",
  "title": "BPLRT Full Sunday Closure — live programme",
  "owner": "Sanjeewa Abeyrathne · D&IS Project Technical Manager",
  "note": "Contract C801B · published from Gantt Studio",
  "openOn": "live",
  "refreshSeconds": 60,
  "allowExports": true
}
```

On GitHub, open `config.json`, press the pencil, replace the contents with what
you copied, and commit. From then on a publish reaches other people's screens
within seconds of them checking.

### 7. What the page opens on

`"openOn": "live"` in `config.json` is what makes the published page open on the
Live carousel rather than the Dashboard. The other tabs are accepted too —
`dash`, `schedule`, `actions`, `teams`, `locs`, `maps`, `org`, `weather` — but on
a wall screen `live` is the one you want.

The carousel does not have to be set up again at this end. Whatever was put on
the Live screen in the desktop copy — the watched groups, subgroups, activities,
maps, org charts and weather boards, which closure was selected and how long
each slide sits — is written into `data/programme.json` when you publish, and
read back here.

### 8. Set how often the wall screen looks

`refreshSeconds` in `config.json` is only where a screen starts. On the **Live**
tab there is a **refresh … s** box beside the play controls. Change it there and
that screen checks at the new interval straight away, and remembers it the next
time it is opened — 15 seconds during a closure, a few minutes the rest of the
week. Anything from 15 seconds to an hour is accepted.

While the Live tab is showing, a new publish is taken **automatically**: the bar
flashes green and the screen rebuilds itself on the new data. Nobody has to be
standing at the wall display. On the Dashboard, the Schedule and every other tab
it behaves as it always has — it says a newer version exists and waits for
**Reload**, so nothing moves under your hands while you are working.

---

## Using it during a closure

1. Open `https://OWNER.github.io/REPO/` on the site laptop.
2. Mark work off exactly as you would in the desktop copy — tick activities
   complete, drag a bar, add a note.
3. The green bar turns to **Not published yet** with a white **Publish changes**
   button, and the gear grows an amber dot. That is the gap between *saved here*
   and *seen by everyone*.
4. Press **Publish changes**.
5. Every open tab picks it up the next time it checks — a screen on the Live tab
   takes it by itself, and the rest are offered a **Reload**. The dashboards, the
   Live carousel and the schedule all rebuild on the new data.

Nothing is lost if you close the laptop mid-closure: your edits autosave into
that browser, and when you come back the page notices the unpublished draft and
offers to open it.

---

## When something goes wrong

The dialog says what GitHub answered and what it usually means. The four you
might actually meet:

| What you see | What it means |
|---|---|
| *GitHub rejected the token (401)* | The token has expired, been revoked, or was pasted short. Make a new one and paste it in again. |
| *The token reaches the repository but is not allowed to write to it (403)* | The token's **Contents** permission is Read-only, or `REPO` was not ticked under Repository access. Edit the token on GitHub or make a new one. |
| *GitHub could not find it (404)* | A typo in the owner, the repository, the branch or the file path. The path is case-sensitive: `data/programme.json`, not `Data/Programme.json`. |
| *The file on GitHub has moved on since this page loaded* | Somebody else published while your page was open. **Load theirs first** takes their version so you can redo your changes on top; **Overwrite it with mine** wins the argument. It will never overwrite them silently. |

If the site itself shows *The programme could not be loaded*, it tells you the
exact address it tried. Nine times in ten the path in `config.json` and the path
in the repository have drifted apart.

---

## What has and has not changed

The file in this repository is the same `Gantt_Studio_RevAN.html` you run on
your desktop, byte for byte. Opened by double-clicking, it is the ordinary
application, saving to that computer. Served over a web address, it becomes the
live page. One file, two lives — there is no separate online build to keep in
step.
