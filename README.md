# Wedding invitation

An animated wedding invitation in a single self-contained HTML file. Open it and a sealed
envelope waits; tap the seal, choose the groom's card or the bride's, and the card it holds
becomes the invitation.

![The invitation card](preview-card.png)

Hemant & Shreya, for real: the names, dates, events and venues live in `index.html`, and
everything else — the reveals, the timeline, the audio — is unchanged by them.

## Running it

There is no build step and no dependencies. Open `index.html` in a browser, or serve the
folder if you want the share links to resolve properly:

```bash
python3 -m http.server 8080
```

Then visit `http://127.0.0.1:8080/`.

## Three independent axes

A guest only ever sees one look — the one set in `LOOK` near the top of the script. Append
`?review=1` to the URL to expose three pickers and try the rest:

| Axis | Options |
|---|---|
| **Design** | `letterpress` · `royal` · `film` · `minimal` · `kinetic` |
| **Theme** | `emerald` · `demon` · `amber` · `orchard` · `coastal` · `plum` · `slate` |
| **Event layout** | `list` (tap to open) · `cards` (swipeable tiles) · `stack` (editorial) |

Any combination can also be linked directly, which is useful for sharing a specific look
with someone:

```
index.html?review=1&design=royal&theme=plum&layout=list
```

None of these parameters survive into the link a guest copies.

## What is in here

- **Two cards behind one seal.** After the reveal, a choice: the groom's invitation carries the
  full celebration, the bride's lists the engagement, wedding and reception. One timeline in
  the markup serves both; the bride's simply hides the groom-only events and reverses the
  name order.
- **A schedule that follows you.** Scrolling the three-day timeline opens whichever event is
  nearest the reading line and closes the rest, with a dead zone and scroll compensation so it
  never fights you, and a short pin after a tap so a deliberate choice wins.
- **A score, not a track.** Continuous bansuri and sitar trading phrases, plus the reveal
  cues, are synthesized in the Web Audio API — see below.
- **Original artwork.** The marigolds, garland, wax seal, mandala and event icons are drawn
  in inline SVG. No image assets ship with the page.

## The audio

There is no audio file. Every note is generated in the browser: a bansuri built from a sine
body with breath noise and delayed vibrato, and a sitar built as a stack of six stretched
partials that each decay at their own rate, its low partials carrying detuned twins for the
jawari shimmer. They trade phrases over a generated convolution reverb.

The melody is drawn from **Bhupali**, the major pentatonic. That is a practical choice as much
as a cultural one: over a fixed tonic every degree of the scale is consonant, so the line can
wander indefinitely without ever landing on a clash — which is what an endlessly looping
background needs.

Nothing autoplays. The audio context is not even created until you tap to open, there is a
mute control from the first screen, your choice is remembered, and a hidden tab suspends
playback.

## Accessibility

Text sits on a 12px floor at weight 400 or above, and every foreground/background pair was
measured against its composited background rather than eyeballed — the lowest ratio in the
default look is 6.9:1, comfortably past WCAG AA. All controls have at least 44px of hit area
and a visible focus ring. Headings are ordered, landmarks are marked, the Devanagari is tagged
`lang="hi"`, decorative SVG is hidden from screen readers, and `prefers-reduced-motion` is
honoured throughout.

## Browser support

Modern evergreen browsers. It leans on `color-mix()`, `:has()`, CSS grid row animation and the
Web Audio API.

## Licence

The code and artwork here are original. The three type families load from Google Fonts and are
licensed under the SIL Open Font License. No licence has been chosen for this repository yet —
add one before sharing it onward.
