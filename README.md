# alekzia.com — how this site works

No CMS, no subscription. The whole site is a folder of files. You edit a file in a text editor, save, re-upload, done. This guide covers everything you'd have clicked buttons for in Squarespace.

## What's in the folder

- `index.html` — the homepage grid
- `ev-icons.html` — a fully built project page (use it as your reference)
- `_template.html` — a blank project page to duplicate for each new project
- `about.html` — bio and contact
- `style.css` — all visual styling for every page, in one file
- `images/` — put every image and thumbnail here

## Previewing locally

Just double-click any `.html` file and it opens in your browser. Edit the file in a text editor (VS Code is free and good — it color-codes everything), save, and refresh the browser tab. That's the whole loop.

## The three edits you'll make most

**A paragraph** is text between `<p>` and `</p>`:

    <p>Your sentence goes here.</p>

Want two paragraphs? Two pairs of tags. Delete a paragraph by deleting the pair and everything between. Italics inside a paragraph: `<em>like this</em>`. A line break without a new paragraph: `<br>`.

**An image**: drop the file into the `images/` folder, then reference it:

    <img src="images/my-photo.jpg" alt="What the image shows" loading="lazy">

The `alt` text is what screen readers announce and what shows if the image fails to load — one plain sentence. Keep filenames lowercase with hyphens, no spaces: `fossil-billboard.jpg`, not `Fossil Billboard FINAL v2.jpg`.

Before uploading, resize images to about 2000px on the long edge and export as JPG around 80% quality. Squarespace did this compression for you invisibly; now it's a 10-second step in Preview (Tools → Adjust Size) or squoosh.app.

**A Vimeo video**: open the video on vimeo.com and copy the number at the end of the URL (e.g. `vimeo.com/123456789` → the ID is `123456789`). Then:

    <div class="video">
      <iframe src="https://player.vimeo.com/video/123456789" title="Film name"
              allow="autoplay; fullscreen; picture-in-picture" allowfullscreen></iframe>
    </div>

The `.video` wrapper keeps it 16:9 and responsive on phones. If a video is private/unlisted on Vimeo, set its privacy to "Hide from Vimeo" + allow embedding on alekzia.com in the video's Privacy settings — it stays unsearchable but plays on your site.

## Adding a whole project

1. Duplicate `_template.html`, rename it (`fossil.html` — lowercase, hyphens, this becomes the URL).
2. Fill in the CAPS placeholders: title, meta line, copy, Vimeo IDs, credits.
3. Open `index.html`, copy one existing `<a class="cell">…</a>` block in the grid, and update its `href`, thumbnail, and text. Grid order = order in the file, so move blocks to rearrange.
4. Drop the thumbnail into `images/` (16:10 crop looks best; anything works, it auto-crops).

For a looping video thumbnail like Rob's site: export a 3–6 second mp4, no audio, under ~5 MB, and use the `<video>` cell variant already in `index.html`.

## Getting your stuff out of Squarespace

- **Images**: Squarespace's export doesn't include galleries reliably. The dependable way is right-click → Save Image on each project page, or grab your originals from wherever you keep them (better quality anyway).
- **Copy**: select and paste from the live pages into the new files.
- **Videos**: already on Vimeo — nothing to move, just collect the IDs.

## Publishing on Netlify

1. Sign up at netlify.com (free tier is plenty for this).
2. "Add new site" → "Deploy manually" → drag this entire folder onto the page. The site is live on a temporary URL in seconds.
3. To update the site later: drag the folder onto the Deploys page again. Every deploy replaces the last, and old versions are kept so you can roll back.

## Pointing alekzia.com at it

1. In Netlify: Domain settings → Add custom domain → alekzia.com. Netlify shows you the DNS records it wants.
2. Where your domain is registered (likely Squarespace Domains): edit DNS — add the A record Netlify gives you for `alekzia.com` and a CNAME for `www`. Netlify provisions HTTPS automatically.
3. Once the domain resolves to Netlify and you've confirmed everything works, cancel the Squarespace **site** subscription. Keep the **domain** registration (or transfer it to a registrar like Cloudflare later — separate, non-urgent decision). Canceling the site plan does not delete your domain, but double-check the domain is on its own billing before you cancel.

## If something breaks

Ninety percent of "the page looks wrong" is an unclosed tag — a `<p>` without a `</p>`, or a deleted `</div>`. Compare your edit against `ev-icons.html`, which is known-good. And since Netlify keeps every previous deploy, the live site can always be rolled back while you fix it.
