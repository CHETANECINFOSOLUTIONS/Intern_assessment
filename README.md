# Entrance tests

Three self-marking entrance tests, served as static HTML. No build step, no
framework, no backend. Deploying is copying four files to a static host.

## What is here

| File | |
|---|---|
| `index.html` | Router. Reads `?track=` and opens the right test. |
| `frontend.html` | Frontend screen — 30 minutes, 20 questions, 100 points |
| `backend.html` | Backend screen — 40 minutes, 20 questions, 100 points |
| `design.html` | Design screen — 40 minutes, 20 questions, 100 points |

## The links to send candidates

```
https://<your-domain>/?track=frontend
https://<your-domain>/?track=backend
https://<your-domain>/?track=design
```

`?track=uiux` and `?track=ux` also reach the design paper. The parameter is
case-insensitive, and `?t=` works as a short form.

A link with no track, or an unrecognised one, shows "this link is missing
something" rather than a menu. That is deliberate — candidates should not be
choosing which paper to sit.

## How a result gets back to you

Each test marks itself in the candidate's browser, then posts the result to a
Google Apps Script web app, which writes one row per candidate into a tab named
after the paper. The endpoint is set in each test file:

```js
var COLLECT_URL = "https://script.google.com/macros/s/.../exec";
```

If that is ever blank, the test still works — it shows the candidate a result
code and a download button to send back by hand. Nothing is lost either way.

To confirm the collector is alive, open the `/exec` URL in a browser. It reports
how many results each tab holds.

## Adding a fourth test

1. Add the new HTML file to this folder.
2. Add one line to `TRACKS` in `index.html`.

That is the whole change.

## Do not commit

**No answer keys, no marking tools, no candidate results.** Everything in this
repo is published to the web the moment it deploys, and the file names are easy
to guess. The answer keys and the Marking Desk live outside this repo, on a
local machine only. `.gitignore` blocks the obvious names, but it cannot save
you from a rename.

The question text and options are necessarily public — a candidate's browser has
to render them. The correct answers are stored as hashes, which stops casual
reading in devtools. That is a deterrent, not a lock; a determined person can
brute-force four known strings. The test is a first filter, not a certificate.
