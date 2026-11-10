# Crystal City Productions — Website

Open `index.html` in any browser to preview. Everything is self-contained (one HTML file + the logo).

```
site/
├── index.html
├── README.md
└── assets/
    ├── logo.png              (original, black background)
    └── logo-transparent.png  (used on the site)
```

There are **no prices on the site**. Pricing lives in the quote form instead: visitors answer a few
questions, and you send a custom number. (The last version with pricing cards is saved one level up in
`_archive/index-with-pricing.html`, outside `site/` so it never gets deployed by accident.)

---

## 1. The quote form

Four short steps, mostly one-tap answers (about 90 seconds):

| Step | Questions |
|---|---|
| 1. Your project | What do you need? (multi) · Which best describes you? · Ongoing or one-time? |
| 2. Scope | How many videos? · Who is filming? · Where would we film? (only if you film) · Where will it be posted? |
| 3. Timing & budget | Extras (multi) · When to start? · Budget range |
| 4. Contact | Name · Email · Phone (optional) · Business / @handle · Questions or anything else (optional) |

Why these: they are the things that actually move a video quote: volume, who shoots and where,
turnaround, add-ons, and budget. "Not sure yet" is always an option so nobody stalls.

**Making submissions arrive.** At the top of the form script (search `QUOTE_ENDPOINT`):

```js
const QUOTE_ENDPOINT = "";   // paste your Formspree URL here
const QUOTE_EMAIL    = "crystalcityprod@gmail.com";
```

- **Empty (default):** submitting opens the visitor's email app with every answer pre-filled, addressed to
  `QUOTE_EMAIL`. It works immediately, but only if they have an email app set up and press send.
- **Filled in:** submissions are sent in the background and land in your inbox, no email app needed.
  Create a free form at formspree.io, copy its URL (looks like `https://formspree.io/f/abcdwxyz`),
  and paste it in. Do this before launch.

**Editing questions.** Each question is a `<fieldset class="q">` in the `#quote` section. A choice is one
`<label class="chip">` line, so add, remove or reword options freely. Radio chips are pick-one; checkbox
chips are pick-many. If you rename a question's `name=""`, update the `collect()` function too.

The budget chips show ranges the *client* picks from. They are not your prices. Delete that question if you
would rather not show any dollar figures at all.

## 2. Work section (Google Drive videos)

Each file in Drive must be set to **Share → General access → "Anyone with the link" → Viewer**, or visitors
see a sign-in box instead of the video. Check in an incognito window.

To add or change videos, edit `const WORK = [` near the bottom of `index.html`:

```js
{ id:"PASTE_DRIVE_FILE_ID", tag:"Real Estate", title:"Listing Tour", ratio:"16/9", size:"full" },
```

- **`id`**: the long string in a Drive link, between `/d/` and `/view`.
- **`ratio`**: `"16/9"` horizontal, `"9/16"` vertical.
- **`size`**: `"wide"` = ⅔ width, `"tall"` = ⅓ (pair with 9/16), `"full"` = full width.

Drive works as a host but it is Google's player. Vimeo or Cloudflare Stream is cleaner long-term.

## 3. Contact details & locations

Email is `crystalcityprod@gmail.com`. Search for `instagram.com/crystalcityproductions` and swap in your real
handle. Dallas–Fort Worth, New York and Los Angeles appear in the hero, services, FAQ, contact and footer,
each paired with a worldwide note.

## 4. Typography

The site runs on **Jost**, a Futura-style geometric sans close to the CRYSTAL CITY wordmark. To try another,
change `--display` and `--sans` in `:root` and the Google Fonts `<link>`. Alternatives: Questrial,
Josefin Sans, Montserrat.

## 5. FAQ policies to confirm

The FAQ states a few policies as placeholders. Edit them to match how you actually work:
month-to-month with 14 days' notice, 50% to book / 50% on delivery for one-offs, client owns all footage,
no travel charge inside DFW / NYC / LA.

## Deploying

No build step, no server. Netlify (drag the `site` folder onto app.netlify.com/drop), Vercel, or GitHub Pages
all work. Point `crystalcityprod.com` at whichever you pick.
