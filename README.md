# North West England — Space Sector Capability Map

A single-file interactive map (Leaflet.js) of space-relevant businesses, academic & research
institutions, infrastructure/facilities and grassroots/public-engagement groups across North
West England, themed for the **North West Space Cluster** (STFC / Sci-Tech Daresbury).

## What it does

- Plots ~47 sourced sites as colour-coded pins across four layers: **Space business**,
  **Academic & research**, **Infrastructure & facilities**, **Grassroots & public engagement** —
  toggle any layer on/off.
- Click a pin to open a detail card: capability tags, a short description, and the specific
  Space North / NWSC opportunity tied to that site.
- **Isolate a district** (Liverpool City Region, Cheshire & Warrington, Greater Manchester,
  Lancashire, Cumbria) to view it on its own, or hit **Show all** to see the North West as one
  connected picture.
- **Cross-district storylines** — four toggleable dashed-line connectors drawn from the research
  doc's own synthesis: the nuclear-to-space-power chain (Warrington → Sellafield → Cumbria →
  Manchester), the two tribology labs, the astronomy corridor, and the "lab to launchpad"
  manufacturing chain. Click one to trace it on the map and read the synthesis note.
- Search box filters pins by name or capability.
- District boundaries are fetched live from the **ONS Open Geography Portal** (Local Authority
  Districts, Dec 2023, UK BUC) — real administrative boundaries, not hand-drawn shapes. If that
  fetch fails (offline, API change), the map still works fully — pins and the base map don't
  depend on it.

## Deploying to GitHub Pages

1. Create a new repo (or use an existing one) and add `index.html` to the root — or to a `/docs`
   folder if you prefer.
2. Push to GitHub.
3. In the repo: **Settings → Pages → Build and deployment → Source: Deploy from a branch**, pick
   `main` and `/` (root) or `/docs`, save.
4. Your map is live at `https://<username>.github.io/<repo-name>/` within a minute or two.

No build step, no dependencies to install — it's one HTML file that loads Leaflet from a CDN.

## Editing the data

Everything site-specific lives in the `SITES` array near the top of the `<script>` block in
`index.html`. Each entry looks like:

```js
{
  id: "daresbury",
  name: "Sci-Tech Daresbury (incl. ESA BIC UK, Hartree Centre, Space Enterprise Lab)",
  category: "infra",                 // business | academic | infra | grassroots
  regionGroup: "Liverpool City Region", // Liverpool City Region | Cheshire & Warrington | Greater Manchester | Lancashire | Cumbria
  lat: 53.3446, lng: -2.6372,
  capabilities: ["ESA Business Incubation (1 of 4 UK sites)", "Hartree supercomputing"],
  description: "...",
  tieIn: "...",                      // the Space North / NWSC opportunity note
  approx: false                      // set true if the coordinate is indicative, not verified
}
```

Add a new object to the array to add a new pin — no other code changes needed. To add a new
cross-district storyline, add an entry to `STORYLINES` with the `id`s of the sites it should
connect, in order.

## Data confidence

Most sites are placed at real, verifiable locations (STFC/university campuses, BAE Systems
sites, Sellafield, named town/venue addresses from the source research). A meaningful number are
still marked `approx: true` — mostly grassroots astronomy societies and community groups placed
at their meeting venue's town rather than an exact address, plus a few companies (SmartIR,
ThinkITTech, James Walker UK) where an exact site wasn't confirmed in the source research. Treat
`approx` pins as indicative only. The sidebar carries the same caveat for anyone viewing it live.

Two administrative-boundary notes carried over from the source research, both reflected in the
data: **Sci-Tech Daresbury (Halton)** is grouped under Liverpool City Region, not Cheshire — it's
sat in the Liverpool City Region Combined Authority since 2014, despite the common assumption.
**Jodrell Bank** sits geographically in Cheshire but is institutionally part of the University of
Manchester — grouped here under Cheshire & Warrington since that's where the physical site is.

## Brand theme

Colours are an approximation of North West Space Cluster / STFC / Sci-Tech Daresbury's visual
style (deep navy plus a warm orange accent) — no official NWSC brand guide or logo file was
found publicly, so this isn't pixel-exact. Swap the `--navy`, `--navy-dark` and `--accent` CSS
variables near the top of `index.html` if you get hold of official values.

## Attribution

- Base map: OpenStreetMap contributors, via CARTO.
- District boundaries: Contains OS data © Crown copyright and database right; Office for
  National Statistics, licensed under the Open Government Licence v3.0.
- Site and opportunity content: compiled from "North West England: Space Sector Capability Map —
  Research Input" (E. Ferguson, July 2026) and North West Space Cluster / STFC / Sci-Tech
  Daresbury public material — not an official Space North or STFC document. See the source
  research doc for the full citation list behind each entry.
