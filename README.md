# 🌼 Kanikonna Kerala

An open-source citizen-science website for documenting **Kanikonna (*Cassia fistula*, the Golden Shower Tree)** across Kerala, India. People can learn about the tree, see recorded trees on a map, and submit their own observations.

This is a **first prototype** built with plain HTML, CSS and JavaScript, using [Leaflet](https://leafletjs.com/) and [OpenStreetMap](https://www.openstreetmap.org/). There is no build step and no server.

## ⚠️ Important: how data is stored

Records are saved in your browser's **local storage**.

- They stay on **your device and browser only**.
- They are **not shared** with other users or devices.
- Clearing browser data deletes them.

The Explore page also has a checkbox that shows **two example cards**. These are demonstrations of the layout, clearly labelled "EXAMPLE", and are **not real or verified tree records**. Map locations come only from coordinates a contributor enters.

## Folder structure

```
kanikonna-kerala/
├── index.html      Home page
├── explore.html    Tree cards, map and location search
├── add.html        Form to submit a tree
├── about.html      About the project
├── css/
│   └── style.css   All styling (colours are variables at the top)
├── js/
│   ├── storage.js  Where records are saved (the only file to change for a database)
│   ├── explore.js  Cards, map markers, search
│   └── add.js      Form validation, photo resizing, saving
├── images/
│   └── kanikonna.svg   Placeholder illustration
└── README.md
```

## Run locally

Option 1: double-click `index.html`. Most things work, but some browsers restrict features for `file://` pages.

Option 2 (recommended): run a tiny local server from the project folder.

```bash
cd kanikonna-kerala
python3 -m http.server 8000
```

Then open <http://localhost:8000>. (Python 3 is needed; VS Code's "Live Server" extension works too.) An internet connection is needed to load the Leaflet library and map tiles.

## Add a real photograph

The home page shows a placeholder illustration until you add a real photo. Save a photo you own, or one with a suitable open licence, as `images/kanikonna.jpg`. The page switches to it automatically. Credit the photographer in this README or under the image. Good sources of openly licensed photos include Wikimedia Commons and iNaturalist (check each photo's licence).

## Deploy free on GitHub Pages

1. Create a free account at <https://github.com> and a new **public** repository (e.g. `kanikonna-kerala`).
2. Upload the contents of this folder (`index.html` must be at the top level of the repository).
3. In the repository go to **Settings → Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch**, select branch `main` and folder `/ (root)`, then **Save**.
5. After a minute or two your site appears at `https://YOUR-USERNAME.github.io/kanikonna-kerala/`.

Other free options that work the same way: Netlify Drop, Cloudflare Pages, or Vercel. Upload the folder, with no build command needed.

## Data format

Each tree is one object (documented at the top of `js/storage.js`):

```json
{
  "id": "tree-1700000000000-ab12c",
  "contributor": "optional name",
  "district": "Kottayam",
  "location": "place name",
  "lat": 9.5916,
  "lng": 76.5222,
  "date": "2026-04-14",
  "photo": "data:image/jpeg;base64,...",
  "flowering": "flowering",
  "notes": "free text",
  "createdAt": "2026-04-14T09:30:00.000Z"
}
```

## Moving to a shared database later

All reading and writing goes through `TreeStore` in `js/storage.js` (`getAll()` and `add()`). To share records between users:

1. Choose a free backend, such as Supabase, Firebase or a Google-Sheets-backed API.
2. Rewrite those two functions to call it (they will become `async`, so add `await` where they are used in `explore.js` and `add.js`).
3. Store photos as files in the backend's storage and keep a URL in `photo` instead of the base64 text.
4. Add moderation so records can be reviewed before they are shown publicly.

## How to contribute

Everyone is welcome: coders, botanists, designers, translators and tree-spotters.

- **Record trees:** once a shared database exists, add real observations from your own visits.
- **Report bugs or suggest ideas:** open a GitHub Issue.
- **Improve the code:** fork the repository, make a small change, and open a Pull Request. Keep it simple and readable for beginners.
- **Translations:** a Malayalam version of the pages would be very welcome.
- **Photos and knowledge:** share openly licensed photographs and local names, uses and stories.

Please keep contributions honest: never invent tree locations or present examples as real data.

## Credits and licence

Map data © [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors. Map library: [Leaflet](https://leafletjs.com/). Suggested licence for the code: MIT (add a `LICENSE` file). Choose a suitable open licence for photos and data.
