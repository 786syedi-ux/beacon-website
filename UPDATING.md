# Keeping the Beacon site updated

This site is static — plain HTML/CSS files, no database, no server code.
That's good for security (nothing to hack into), but it means "updating
it" always means: **edit the files → redeploy the whole folder.** There's
no live "admin panel" to log into.

## The two ways to make changes

### A — Ask Claude, then redeploy (simplest, no technical skill needed)
1. Tell Claude what to change (new team member, updated stat, a typo, a
   new Insights article, whatever).
2. Claude edits the files and gives you a fresh `beacon-site.zip`.
3. Unzip it, and drag the **whole folder** onto your host's dashboard:
   - **Netlify:** Site → Deploys tab → drag the folder into the drop
     zone. This replaces the live site in ~10 seconds.
   - **Cloudflare Pages:** Site → Deployments → Create deployment →
     upload the folder.
4. Done. No git, no code editor required.

**Important:** always redeploy the *entire* folder, never just one file.
If you ever hand-edit a file locally, make sure that's the copy you
redeploy from — don't mix an old zip with a new one, or you'll silently
overwrite recent changes.

### B — Git-connected deploy (better long-term, worth setting up once)
If you push the site to a GitHub repo and connect that repo to Netlify
(or Cloudflare Pages), every update becomes `git push` and the site
redeploys itself automatically — and you get full version history, so
you can always roll back to yesterday's version if something breaks.
This is one-time setup effort in exchange for less friction on every
update after that. Ask Claude to walk you through it whenever you're
ready — it's about 15 minutes.

## Adding a new Insights article
This was built to be the lowest-friction update on the whole site:
1. Send Claude the topic or the report/article that prompted it.
2. Claude researches it, writes it in the existing format (cited
   sources, a point of view, linked to the right practice page), and
   regenerates `insights.html` plus the new article page.
3. Redeploy as in option A above.

## Routine content edits you can do yourself
If you're comfortable opening an HTML file in a plain text editor
(Notepad, TextEdit, VS Code — not Word), most text on the site is easy
to find and change directly:
- Open the relevant `.html` file
- Use Find (Ctrl/Cmd+F) for the text you want to change
- Edit only the text *between* tags, e.g. change
  `<h1>Old headline</h1>` to `<h1>New headline</h1>` — never delete the
  `<...>` tags themselves, or the page layout will break
- Save, then redeploy (option A above)

For anything structural — new sections, new pages, changed layout — ask
Claude rather than hand-editing; it's easy to break the CSS classes the
design depends on.

## Placeholder values still to replace
These were left as clearly-marked placeholders and need your real
details once you have them:

| Placeholder | Found in | Replace with |
|---|---|---|
| `beaconhc.com` | `sitemap.xml`, footer email, meta tags | your real domain |
| `hello@beaconhc.com` | contact section, footer | your real business email |
| `G-XXXXXXXXXX` | every page's `<head>` | your GA4 Measurement ID |
| `REPLACE_WITH_YOUR_SEARCH_CONSOLE_CODE` | every page's `<head>` | your Search Console verification code |

Ask Claude to do a find-and-replace across all files once you have
these — it's a five-minute job.

## A light maintenance cadence
Nothing here needs daily attention. A reasonable rhythm:
- **Monthly:** skim Google Search Console for crawl errors or security
  warnings; check the contact form is still landing in your inbox
- **Quarterly:** review the Insights section — is anything stale or
  superseded by newer research; add one new piece if relevant
- **As it happens:** new role, new certification, a real client
  testimonial once you have one — send it to Claude to add
