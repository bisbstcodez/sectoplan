# Sectograph

A 24-hour circular day planner. Runs as a single static page, syncs across devices
through a GitHub gist, and installs to a phone or tablet home screen.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole app — markup, styles, and logic |
| `manifest.webmanifest` | Makes the page installable; sets name, colors, icons |
| `sw.js` | Service worker; caches the app so it opens without signal |
| `apple-touch-icon.png` | Home screen icon for iPhone and iPad (180px) |
| `icon-192.png`, `icon-512.png` | Icons for Android and desktop installs |
| `icon-maskable-512.png` | Android adaptive icon |
| `favicon-32.png`, `icon.svg` | Browser tab icon |

All files sit in the repository root, next to each other. The paths are relative,
so the project works under a subpath like `username.github.io/sectoplan/`.

## Add to your iPhone or iPad home screen

You have to use **Safari** — Chrome on iOS can't install web apps.

1. Open your Pages URL in Safari.
2. Tap the **Share** button (the square with an arrow pointing up).
3. Scroll down and tap **Add to Home Screen**.
4. The name and icon appear. Tap **Add**.

The app now opens full screen with no browser bar, and its own icon in the app
switcher. Repeat on each device.

If the icon still looks like a screenshot of the page, Safari cached the old
version. Close the tab, clear the site data under Settings → Safari → Advanced →
Website Data, then reload and try again.

## Add to an Android home screen

Open the URL in Chrome, tap the **⋮** menu, then **Install app** or
**Add to Home screen**.

## Add to a Mac or Windows desktop

In Chrome or Edge, open the URL and click the install icon at the right edge of
the address bar. In Safari on macOS, use **File → Add to Dock**.

## Turn on sync

Without this the app works fine, but each device keeps its own separate copy.

1. Go to [gist.github.com](https://gist.github.com). Name the file
   `sectograph.json` and put `{}` in the body. Create it as a secret gist.
   Copy the long ID from the URL.
2. Go to [github.com/settings/tokens](https://github.com/settings/tokens) →
   **Fine-grained tokens** → **Generate new token**. Under **Account
   permissions**, set **Gists** to **Read and write**. Generate it and copy the
   token — GitHub shows it only once.
3. In the app, tap the **gear** icon. Paste the gist ID and the token. Tap
   **Save**.

Repeat step 3 on every device. The gist ID and token live in each browser's own
storage and are never committed to this repository.

The app pulls when it opens and when you switch back to it, and pushes a few
moments after each change. Last write wins, so avoid editing the same day on two
devices at once.

## Using it

- **+** adds an activity: name, start, end or duration, ring, and color.
- **Drag a sector** around the dial to move it. **Drag an end handle** to resize.
  Changes snap to five minutes.
- **Rings** let overlapping activities sit side by side instead of on top of each
  other.
- **Repeat** builds recurring activities — daily, weekly with specific weekdays,
  monthly, or yearly, ending never, after a number of times, or on a date.
- Editing a repeating activity changes every occurrence. Dragging one occurrence
  changes only that day. Deleting asks which you meant.
- The **calendar** icon switches to the month grid. Each day is a ring showing
  that day at a glance. Tap one to open it.
- Tap the date heading to jump back to today.

## Offline

The service worker caches the app itself, so it opens with no connection and your
schedule renders from local storage. Syncing resumes when you're back online.

After you push a change to the repository, an installed copy may run the old
version once before updating. Open it twice, or pull down to refresh in the
browser.
