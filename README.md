# Fab Makes Videos

Single-page portfolio site. Plain HTML, CSS, and JavaScript with no build step.

## Structure

```
index.html              # the whole site
assets/
  fonts/Grift-VariableVF.ttf
  posters/work-1..4.jpg  # poster frame shown before hover
  videos/work-1..4.mp4   # muted loop preview, plays on hover
```

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

## Replacing the videos

Swap the files in `assets/videos/` (keep the names `work-1.mp4` ... `work-4.mp4`) and the matching poster frames in `assets/posters/`. Use web-optimized H.264 MP4, muted, short loops, ideally a few MB each. Update the titles and categories in `index.html` if needed.
