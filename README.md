# Talkback S-1 — Dictation Unit

A speech-to-text app that runs entirely in the browser. No server, no API
key, no build step — it's a single `index.html`.

## Host it on GitHub Pages

1. Create a new **public** GitHub repo (e.g. `talkback-s1`).
2. Add `index.html` and `apple-touch-icon.png` to the repo root.
3. Go to **Settings → Pages**. Under "Build and deployment", set
   **Source: Deploy from a branch**, branch `main`, folder `/ (root)`. Save.
4. Wait a minute, then your app is live at:
   `https://<your-username>.github.io/talkback-s1/`

## Adding it to your iPhone home screen

1. Open that URL in **Safari** on your iPhone.
2. Tap the Share icon → **Add to Home Screen**.
3. You'll get an app icon on your home screen. Tapping it opens the page
   in Safari (address bar visible) rather than a chrome-free "app" window.

**This is intentional, not a bug in the setup.** iOS has a long-standing,
unfixed WebKit limitation ([bug 185448](https://bugs.webkit.org/show_bug.cgi?id=185448)):
when a web page is launched in **standalone mode** (the fullscreen,
no-address-bar mode that `apple-mobile-web-app-capable` or a
`display: standalone` manifest triggers), the microphone and speech
recognition APIs silently stop working — the permission prompt never
even fires. It works fine in regular Safari, including when Safari was
opened from a home screen icon.

So this build skips the standalone/manifest setup on purpose, to keep the
one feature that matters. You still get a tappable icon and a clean
recording screen — you'll just see Safari's address bar at the top.

If you ever want the fullscreen "no browser chrome" look badly enough to
give up in-browser dictation, the only real fix is a native iOS app using
Apple's own Speech framework — that's a different project (Swift, Xcode,
App Store or TestFlight), not a tweak to this one.

## Notes

- Works in: Safari on iOS/iPadOS, Chrome/Edge on desktop, Chrome on Android.
- Does not work in: Firefox (no Web Speech API support), desktop Safari
  speech recognition is inconsistent across macOS versions.
- Needs HTTPS to access the microphone — GitHub Pages serves over HTTPS
  automatically, so no extra setup is needed there.
- Nothing is uploaded to any server you control — audio goes only to the
  browser's own speech engine (on iOS/Safari that's Apple's, on
  Chrome that's Google's), the same as typing with dictation anywhere else
  on the device.
