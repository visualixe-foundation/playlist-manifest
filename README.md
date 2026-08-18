# Manifest — Playlist Cataloger

A static webpage that reads a YouTube playlist (public, unlisted, or private)
and exports every track's title + channel as a .txt or Spotify-search list.
No audio or video is ever downloaded.

**Live site:** https://playlist-manifest.vercel.app

## Public / Unlisted playlists

Works out of the box. Just paste the playlist link and click **Build manifest**.
(Optional: users can add their own YouTube Data API key for heavy use.)

## Private playlists

Users only need to click **Sign in with Google** (with the account that owns the playlist).

### One-time setup (site owner only)

Private support needs a Google OAuth Client ID. Do this once:

1. Go to https://console.cloud.google.com/apis/credentials
2. **Create Credentials → OAuth client ID** → Application type: **Web application**
3. Under **Authorized JavaScript origins**, add:
   - `https://playlist-manifest.vercel.app`
   - (optional) `http://localhost:3000` for local testing
4. You may be asked to configure the **OAuth consent screen** first — choose **External**, fill the required fields, and add your own Google account under **Test users**.
5. Copy the generated **Client ID**.
6. Open `index.html` and replace the placeholder:

```js
const OAUTH_CLIENT_ID = "YOUR_CLIENT_ID_HERE.apps.googleusercontent.com";
```

with your real Client ID. Redeploy (or push to GitHub if Vercel is connected).

After that, anyone can use the Private tab by simply signing in with Google — no extra steps for them.

## Notes

- Nothing here touches audio/video files — it only reads the same title, channel, and duration metadata visible on the playlist page via YouTube’s official API.
- Handles playlists of any size (paginates automatically).
- A video’s “channel” is the closest thing YouTube’s public API exposes to a credited artist for regular uploads.
