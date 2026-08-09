# Manifest — Playlist Cataloger

A static webpage that reads a YouTube playlist (public, unlisted, or private)
and exports every track's title + channel as a .txt, .csv, or Spotify-search
list. No audio or video is ever downloaded.

## Deploy to Vercel (no coding needed)

**Option A — drag and drop (easiest):**
1. Go to https://vercel.com/new
2. Sign in / sign up (free).
3. Drag this whole folder onto the page, or click to browse and select it.
4. Click **Deploy**. Vercel will give you a live URL like
   `https://your-project.vercel.app` in under a minute.

**Option B — Vercel CLI:**
```bash
npm i -g vercel
cd playlist-manifest
vercel
```
Follow the prompts (accept defaults — it's a static site, no build step).

## Using it for public / unlisted playlists

1. Get a free YouTube Data API key:
   - https://console.cloud.google.com/apis/library/youtube.googleapis.com
   - Click **Enable**
   - **Credentials → Create Credentials → API key**
2. Paste that key into the "Public / Unlisted" tab on the site.
3. Paste the playlist link, click **Build manifest**.

This mode works immediately on any domain — no extra setup.

## Using it for a private playlist

Private playlists can only be read by the account that owns them, so this
mode needs you to sign in with Google. This requires a one-time setup
**after you know your Vercel URL**:

1. In the same Google Cloud project, go to
   https://console.cloud.google.com/apis/credentials
2. **Create Credentials → OAuth client ID** → Application type: **Web application**.
3. Under **Authorized JavaScript origins**, add your deployed URL exactly,
   e.g. `https://your-project.vercel.app` (and `http://localhost:3000` if
   you want to test locally). No trailing slash.
4. You may be prompted to configure the **OAuth consent screen** first —
   choose **External**, fill in the required fields, and add your own
   Google account under **Test users** (this keeps it free and avoids
   Google's app-review process, since only you will ever use it).
5. Copy the generated **Client ID** and paste it into the "Private" tab on
   the site.
6. Click the sign-in button, approve access, then paste the playlist link
   and click **Build manifest**.

## Notes

- Nothing here touches audio/video files — it only reads the same title,
  channel, and duration metadata visible on the playlist page, via
  YouTube's official API.
- Handles playlists of any size (paginates automatically — tested logic
  for 500+ items).
- A video's "channel" is the closest thing YouTube's public API exposes to
  a credited artist for regular uploads. Many music uploads already put
  the artist in the title itself (e.g. "Artist - Song"), which is included
  too.
