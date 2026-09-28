# Shamama — A Retrospective

A standalone, offline birthday website — a private exhibition, walked
room by room. Pure HTML, CSS and vanilla JavaScript. No build step, no
install, no backend.

```
birthday-shamama/
├── index.html
├── css/style.css
├── js/script.js
├── images/        ← photo1.jpg … photo10.jpg (placeholders already inside)
├── videos/        ← video1.mp4, video2.mp4, video3.mp4 (you add these)
└── audio/         ← birthday-song.mp3 (you add this)
```

## 1. Open it in VS Code

1. Open the `birthday-shamama` folder in VS Code (`File → Open Folder…`).
2. Install the **Live Server** extension (search "Live Server" by Ritwick
   Dey in the Extensions panel).
3. Right-click `index.html` → **Open with Live Server**. It reloads
   automatically every time you save a file.

You can also just double-click `index.html` to open it straight in a
browser — every path is relative, so no server is required at all.

## 2. The five rooms

| Room | Section id | What it is |
|---|---|---|
| I | `#entrance` | The title wall — her name, the message |
| II | `#collection` | The gallery wall — photos and videos |
| III | `#guestbook` | **Her Name** — her memories orbit; catch seven and set each into a letter |
| IV | `#correspondence` | Three letters, opened by "breaking the seal" |
| V | `#reveal` | The final room, behind the "Unveil It" button |

## 3. Add Shamama's real photos

Drop her photos into `images/`, named exactly:

```
photo1.jpg  photo2.jpg  photo3.jpg … photo10.jpg
```

They replace the placeholder plates automatically — nothing in the code
needs to change. `.jpg`, `.png` and `.webp` all work; if you use a
different extension, update the matching filename in `js/script.js`
(see below).

## 4. Edit photos, videos, captions and the gallery hang

Open `js/script.js` and find the `PHOTOS` and `VIDEOS` arrays near the
top:

```js
const PHOTOS = [
  { file: "photo1.jpg", caption: "My favourite human" },
  { file: "photo2.jpg", caption: "Always silly" },
  // ...
];
```

Edit a `caption`, add a new `{ file: ..., caption: ... }` line, or
delete one you don't need.

Just below that is `WALL_LAYOUT` — this is what actually decides the
order and size of frames on the gallery wall in Room II:

```js
const WALL_LAYOUT = [
  { media: PHOTOS[0], size: "wide" },
  { media: VIDEOS[0], size: "feature" },
  { media: PHOTOS[1], size: "square" },
  // ...
];
```

`size` can be `"wide"`, `"feature"`, `"portrait"` or `"square"` — that's
what gives the wall its asymmetric, hand-hung look. Reorder the lines,
swap which photo goes where, or change a size to rebalance the wall.

## 5. Add the 3 videos

Drop three short clips into `videos/`, named `video1.mp4`, `video2.mp4`,
`video3.mp4`. Until they're added, clicking a video frame shows a
gentle "add this file" message instead of a broken player.

## 6. Add the birthday song

Drop an MP3 into `audio/birthday-song.mp3`. The player in the
bottom-right corner picks it up automatically — nothing autoplays,
Shamama has to press play herself. To rename the song title shown
there, change `SONG_TITLE` near the top of `js/script.js`.

## 7. Her Name room, the floating memories, and the letters

**Her Name (Room III).** Every photo and video in `PHOTOS` / `VIDEOS`
(section 4) orbits her name as a small card. Drag one into a letter — or
just tap it and it flies to the next empty one — and the letter develops
into that photograph, or plays that video. Seven memories later the name
is made of her. Click a finished letter to send its memory back into
orbit. The spelled name is the `NAME` constant near the top of
`js/script.js`; the room's heading and hint are in `index.html`.

**Floating background.** Faint, feathered copies of the same photos and
(on desktop) two of the videos drift up behind every room. Their
transparency is set in `setupDrift()` in `js/script.js` (`--o`, roughly
0.13–0.24 — raise the numbers to make them more visible). Videos are
muted; missing files are simply skipped. The "reduce motion" pill (and
the OS setting) freezes all of it.

**Letters (Room IV).** `LETTERS` is a list of `{ title, body }` entries —
edit the text directly.

## 8. Change the title wall message

This lives in `index.html` — search for `entrance__title` and edit the
text around it:

```html
<h1 class="entrance__title">Shamama</h1>
<p class="entrance__subtitle">a retrospective, in her honour</p>
...
<p class="entrance__message">To more laughter, brighter days, beautiful memories, and all the dreams you chase.</p>
```

The final message ("Happy Birthday, Shamama! ♡" / "You deserve all the
beautiful things life has to offer.") lives in the same file, in the
`#revealOverlay` block near the bottom of `<body>`.

## 9. Colors & fonts

All colors are CSS variables at the top of `css/style.css`, under
`:root { ... }` — `--ink`, `--brass`, `--ivory`, `--wine`, etc. Fonts
are loaded from Google Fonts in the `<head>` of `index.html` (Fraunces
for headings and letters, Archivo for everything else); swap the font
names there and in the `--font-*` variables in `style.css` if you'd
rather use something else.

## 10. Publishing it on GitHub Pages

1. Create a new (private, if you'd like) GitHub repo and push this
   folder to it, with `index.html` at the root of the repo.
2. In the repo, go to **Settings → Pages**, set the source branch to
   `main` and the folder to `/ (root)`.
3. GitHub gives you a link a minute or two later — that's the one to
   send Shamama.

## A few details already built in

- **Reduce motion** — a small pill in the bottom-left corner turns off
  the ambient drift and flicker, and the site also respects the
  OS-level "reduce motion" setting automatically.
- **Keyboard support** — arrow keys move between photos in the
  lightbox, Escape closes whatever's open.
- **Mobile** — the gallery wall, nav and every room reflow for small
  screens; no horizontal scrolling.
- **Missing files never look broken** — a photo, video or song that
  hasn't been added yet shows a soft placeholder or a friendly note
  instead of an error icon.

Happy birthday, Shamama. ♡
