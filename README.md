# We Were Here

A public digital archive of the African American experience in Danville and Boyle County, Kentucky — oral histories, photographs, and documents gathered with the Danville-Boyle County African American Historical Society and Centre College.

**Live site: [wewerehere.omeka.net](https://wewerehere.omeka.net)**

The catalogue itself runs on Omeka Classic. This repository holds everything Omeka could not: durable hosting for the archive's media, and the custom players embedded in the site.

## The archive at a glance

| | |
| --- | --- |
| Catalogued items | 855 |
| Oral-history audio clips | 386, across 11 themes |
| Narrated photographs (video) | 151 |
| Interviewee portraits | 34 |
| Item photographs | 275 |

## Players

Three self-contained pages — vanilla JavaScript, no framework, no build step, no dependencies. Each is embedded in the archive as an iframe and reports its own height back to the host page via `postMessage`, so the surrounding Omeka page resizes to fit instead of scrolling inside a fixed box.

- **`player.html`** — *Narrated Memories.* Shuffles 386 audio clips drawn from the oral histories, grouped into 11 themed stations (Second Street, Businesses, Churches, Schools, Urban Renewal, and more). Every clip is paired with a photograph. Reads `stations.json`.
- **`narrated.html`** — *Narrated Photographs.* Shuffle player for 151 short videos in which a narrator speaks over a single photograph.
- **`listen.html`** — a compact standalone build of the shuffle player, with its playlist embedded directly in the file so it runs from any static host.

## Layout

```
player.html        Narrated Memories player  (reads stations.json)
narrated.html      Narrated Photographs shuffle player
listen.html        standalone shuffle player (self-contained)
stations.json      386 clips across 11 stations, each with audio + photo
manifest.json      playlist for listen.html
audio/             386 oral-history clips (mp3)
items/             275 item photographs
portraits/         34 interviewee portraits + site hero image
paper/             the peer-reviewed article describing the project
```

## Notes on the build

- **Durable media URLs.** Omeka's own file URLs expire, which broke image cards on the live site. Media is served from this repository instead — item photographs over `raw.githubusercontent.com`, and audio through the jsDelivr CDN, which handles range requests properly for seeking.
- **Themed shuffle.** `stations.json` maps every clip to a theme and a photograph, so the player can shuffle within a station or across the whole archive. Order is randomized client-side with a Fisher–Yates shuffle.
- **Embedding constraints.** The host is a hosted Omeka Classic install with a sanitizing stylesheet editor, so the players carry their own styles inline and communicate with the parent page only through `postMessage`.

## Credits

The oral histories belong to the narrators and to the Danville-Boyle County African American Historical Society. The project was carried out in partnership with the Society and Centre College's Anthropology program.

The article in `paper/` is published in *Annals of Anthropological Practice* 49(2), 2025 (© American Anthropological Association) and is included with the author's permission.
