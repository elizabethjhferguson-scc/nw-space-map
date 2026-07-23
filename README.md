# North West England — Space Industry Capability Map

A single-file interactive map (Leaflet.js) of space-relevant academia, research, industry,
industry-adjacent organisations and space companies across North West England, built to
support the Space North / North West Space Cluster bridging proposal.

## What it does

- Plots every notable site as a colour-coded pin across five layers: **Academia**, **Research**,
  **Industry**, **Industry-adjacent**, **Space companies** — toggle any layer on/off.
- Click a pin to open a detail card: capability tags, a short description, and the specific
  Space North / SHY opportunity tied to that site.
- **Isolate a region** (Cumbria, Lancashire, Cheshire, Greater Manchester, Merseyside) to view it
  on its own, or hit **Show all** to see the North West as one connected picture — the map to
  visualise the "bottom-up" build of Space North (region → academia/research/industry →
  cross-region collaboration).
- Search box filters pins by name or capability.
- Region boundaries are fetched live from the **ONS Open Geography Portal** (Local Authority
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
  name: "Sci-Tech Daresbury & ESA Business Incubation Centre UK",
  category: "research",              // academia | research | industry | adjacent | space
  regionGroup: "Cheshire",           // Cumbria | Lancashire | Cheshire | Greater Manchester | Merseyside
  lat: 53.3446, lng: -2.6372,
  capabilities: ["STFC National Laboratory", "ESA Business Incubation (1 of 4 UK sites)"],
  description: "...",
  tieIn: "...",                      // the Space North / SHY opportunity note
  approx: false                      // set true if the coordinate is indicative, not verified
}
```

Add a new object to the array to add a new pin — no other code changes needed.

## Data confidence

Most sites are placed at their real, verifiable coordinates (STFC/university campuses, BAE
Systems sites, Sellafield). Two entries — **North West Aerospace Alliance** and **Smart IR** —
are marked `approx: true` because I could not confirm an exact site address; treat their
positions as indicative only and verify before using this for anything beyond internal
discussion. The bottom of the map's sidebar carries the same caveat for anyone viewing it live.

## Attribution

- Base map: OpenStreetMap contributors, via CARTO.
- Region boundaries: Contains OS data © Crown copyright and database right; Office for National
  Statistics licensed under the Open Government Licence v3.0.
- Site and opportunity content: compiled from Space Hub Yorkshire / Space North public material
  and general research — not an official Space North or STFC document.
