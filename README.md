# Fab Makes Videos

Single-page portfolio site. Plain HTML, CSS, and JavaScript with no build step.

Live at https://www.fabmakesvideo.com (hosted on Vercel, domain at Namecheap).

## How to update the site later

The whole site is one file: `index.html`. After any change, you publish with three commands (see "Publish your changes" at the bottom). Here are the common edits.

### Add or change videos in a category

1. Open `index.html` in any text editor.
2. Find the block that starts with `var WORK = {`. Each category is a list of videos that looks like this:

   ```js
   events: { label: "Events", videos: [
     { title: "Female Foundry Event", url: "https://www.youtube.com/watch?v=pm4x2bvWZzc" },
     { title: "Bolt Summit 2025",     url: "https://www.youtube.com/watch?v=Ue8tDZkp8LY" }
   ]},
   ```

3. To add a video, copy one `{ title: "...", url: "..." }` line, paste it on its own line inside the same category's `[ ... ]`, and put a comma after every line except the last. Use the normal YouTube or Vimeo link.
4. To remove a video, delete its line (and fix the commas so the last line has none).
5. Save. The tile's "X videos" count updates by itself.

The four categories are `events`, `commercial`, `documentary`, and `testimonials`. To rename one, change its `label: "..."` and also the matching word in the tiles further up the file (the `<span class="title">` text), plus the alt text.

### Change a category thumbnail

Replace the matching file in `assets/thumbnails/` keeping the exact name:

```
assets/thumbnails/events.jpg
assets/thumbnails/commercial.jpg
assets/thumbnails/documentary.jpg
assets/thumbnails/testimonials.jpg
```

Use a 16:9 image. Smaller is better (aim for under ~300 KB).

### Edit text (name, about, contact)

Open `index.html` and search for the text you want to change (for example "Fab is based in London") and edit it in place. The marquee words live in the block with `class="marquee__track"`.

### Publish your changes

In Terminal:

```
cd ~/Claude/"Fab Makes Videos"
git add -A
git commit -m "update videos"
git push
```

Vercel redeploys automatically within a minute, and the live site updates. (Hard-refresh your browser with Cmd+Shift+R if you still see the old version.)

## Structure

```
index.html                    # the whole site
assets/
  fonts/                      # Grift (sans) + Editorial Today (display serif)
  thumbnails/                 # one image per category tile
```

Videos are not stored in the repo, they stream from YouTube/Vimeo via the links in the `WORK` block inside `index.html`.

All paths are relative, so the site works when opened locally or hosted anywhere with zero configuration.

## Preview locally

Open `index.html` in a browser. The custom cursor and hover-to-play previews only work in a real browser, not a file preview pane.

## Deploy with GitHub + Vercel

1. Create a new GitHub repo and push these files to it.
   ```
   git init
   git add .
   git commit -m "Initial portfolio"
   git branch -M main
   git remote add origin https://github.com/<you>/<repo>.git
   git push -u origin main
   ```
2. Go to vercel.com, "Add New Project", import the repo.
3. Framework preset: "Other". No build command, no output directory. Deploy.

## Connect the domain (bought at Namecheap)

1. In the Vercel project: Settings then Domains.
2. Add `fabmakesvideo.com` and `www.fabmakesvideo.com`. Pick which one is primary; the other redirects.
3. Vercel shows the DNS records to create. In Namecheap: Domain List then Manage then Advanced DNS, and add them:
   - Root `fabmakesvideo.com`: A record to the IP Vercel gives you.
   - `www`: CNAME to the target Vercel gives you.
4. Wait for it to verify (usually minutes). SSL is issued automatically.

## Category thumbnails

Each work tile shows an image from `assets/thumbnails/`. Drop your four frames in there with these exact names (16:9 JPG recommended):

```
assets/thumbnails/events.jpg
assets/thumbnails/commercial.jpg
assets/thumbnails/documentary.jpg
assets/thumbnails/testimonials.jpg
```

If a file is missing, the tile falls back to a YouTube thumbnail automatically.
