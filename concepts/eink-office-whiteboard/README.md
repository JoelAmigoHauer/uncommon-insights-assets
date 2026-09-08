# Ambient e-paper whiteboard: concept and cost reality

Working note, September 2026. Uncommon Insights / We Are Visionists.

## The one-line version

A zoomable e-ink whiteboard at $15 COGS is off by 30 to 60 times, so the product that
actually works at that price is a small tile sold in multiples, where the zoom lives in
the phone and the wall of tiles is the canvas.

---

## 1. Two premises worth correcting first

### E-paper is not cheap to make, and it never was

E Ink Holdings guided full-year FY2026 gross margin at 55 to 59 percent, up from 50
percent in 2024. That is monopoly pricing on a technology with essentially one supplier
of the front plane. A company running 59 percent gross margin has no reason to pass
manufacturing savings down the chain, and it has not.

E-paper won the handheld market on bistability and reflectivity. Zero power to hold an
image gave the Kindle weeks of battery, and a reflective surface gave it sunlight
readability. Manufacturing cost had nothing to do with it. The Kindle got cheap for three
separate reasons: one fixed small size held for a decade, tens of millions of units on
that one SKU, and Amazon subsidising the hardware against content margin.

The lesson to take from that is useful and it is the opposite of the intuition. Pick one
small size. Make an enormous number of them. Earn on something other than the panel.

### Cost scales worse than area

E-paper front planes are made on repurposed LCD lines with IGZO backplanes. Yield falls
as substrate area grows, and every defect scraps a whole sheet. Published reference
points, September 2026:

| Size | Product | Price | Active area | Implied $/in² |
|---|---|---|---|---|
| 2.13" | ESL, full retail unit incl. radio + battery + case | $4.25 to $7 | ~1.9 in² | n/a (finished good) |
| 4.2" mono | Waveshare retail module | $17 to $19 | ~8.5 in² | ~$2.10 retail |
| 7.5" mono | Waveshare retail HAT | $51 to $57 | ~24 in² | ~$2.20 retail |
| 13.3" Spectra 6 | E Ink official shop | $449 | ~85 in² | ~$5.28 retail |
| 25.3" Spectra 6 | E Ink official shop | $1,400 | ~310 in² | ~$4.52 retail |

Retail module prices carry roughly 2.5 to 3.5 times markup over a direct panel buy at
volume. Working the numbers back, a mono panel bought direct at 10k units lands near
$0.55 to $0.80 per square inch below 10 inches, and climbs steeply above it.

**What that means for a whiteboard.** A modest 24-inch diagonal board has about 247 square
inches of active area. Panel alone, before any electronics, enclosure, battery, assembly
or packaging, is $430 to $600 at volume. The stated target for the entire finished good
is $15.

### The zoom requirement fights the physics

E-paper refreshes at 1 Hz or slower. A full refresh runs a black-white-black inversion
cycle to clear ghosting, and it is visible. Partial refresh is faster and accumulates
residual artefacts that get worse the more you use it. This is a property of moving
charged pigment through a fluid, and no amount of software fixes it.

Continuous pan and zoom on e-paper is a bad experience at any price. Anyone who has tried
to scroll a PDF on a Boox knows the feeling.

---

## 2. What the shelf already looks like

| Product | Screen | RRP | Notes |
|---|---|---|---|
| TRMNL (OG) | 7.5" mono e-paper | $139, down to $99 at 151+ units | Closest comparable. ESP32 + panel + plastic case, optional plan |
| TRMNL X | Larger e-paper | $229, $189 at volume | |
| Vestaboard Note | Split-flap | $1,099 frameless, from 1 Sep 2026 | |
| Vestaboard | Split-flap, 132 tiles | $3,499 | Plus a Vestaboard+ subscription |
| Boogie Board | 8.5" cholesteric LC | ~$30 | Writable, bulk erase only, no addressing |
| Boox Mira / Dasung | 13.3" to 25.3" e-paper monitor | $800 to $2,500 | |

The $17 to $90 band is empty of anything with a network-addressable persistent display.
That gap is real, and it is empty because of the panel cost curve above, not because
nobody thought of it.

---

## 3. Option A: the tile system

Sell a small e-paper tile. Sell it in multiples. Put the zoom in the phone.

### The mechanic

One canvas lives in the cloud. Every tile holds a position on that canvas as an
`(x, y, zoom)` triple. You pinch-zoom on your phone, and every tile re-renders to show
its slice of the new framing.

Zoomed out, the wall shows the quarter. Zoomed in, the same wall shows one project. The
tiles refresh in a staggered wave over 1 to 2 seconds, so the wall visibly *settles* into
the new view. E-paper's slow refresh becomes a physical event you watch happen, which is
the thing a glass screen cannot do.

Buy one tile for your desk. Buy six for the wall behind you. Buy twenty for the team
room. The whiteboard is emergent.

### BOM, 4.2 inch tile

| Line item | @ 10k units | @ 50k units |
|---|---|---|
| 4.2" mono e-paper panel + FPC | $6.20 | $4.95 |
| ESP32-C3 module (Wi-Fi + BLE, RISC-V) | $1.35 | $1.10 |
| 4-layer PCB, passives, connectors | $1.40 | $1.05 |
| Li-po 1500 mAh + protection circuit | $2.10 | $1.75 |
| ABS enclosure, 2-part injection moulded | $1.90 | $1.35 |
| Magnet mount, steel plate, VHB adhesive | $0.55 | $0.42 |
| USB-C receptacle + charge IC | $0.45 | $0.35 |
| Assembly, test, firmware flash | $1.30 | $0.95 |
| Retail carton, insert, manual | $0.95 | $0.70 |
| **Total** | **$16.20** | **$12.62** |

The 10k build misses the $15 target. The 50k build clears it. A 2.9-inch version clears it
at 10k, landing near $11.60, and that is the honest answer for a first production run.

### Pricing

| | Entry | Target |
|---|---|---|
| Single tile RRP | $49 | |
| Six-pack RRP | $239 | The actual product |
| Twenty-tile team wall | $749 | |
| Canvas plan, per seat | $6/month | Where the money is |

At $49 RRP and $15 COGS you have $34 gross. Freight, duty and returns take $8 to $12.
DTC customer acquisition takes $15 to $25. Unit one loses money. Every business at this
price point is a subscription business or a multi-unit AOV business, and this one has to
be both.

### Risks

1. **Panel supply.** One supplier, 59 percent gross margin, and you are a small customer.
   Negotiate an annual volume commitment or accept price at their discretion.
2. **Six tiles is not a whiteboard.** Six 4.2-inch tiles give 51 square inches of active
   area across a 220 by 255 mm footprint. Persuading someone that is a whiteboard is a
   marketing problem, and it might be an unsolvable one.
3. **Bezels.** Every tile has a border. A wall of tiles reads as a wall of tiles, and
   the seams are visible from across the room.

---

## 4. Option B: the cholesteric slate

Use Kent Displays' Reflex cholesteric liquid crystal film. Roll-to-roll printed on
flexible plastic in the US, which is the one genuinely low-cost bistable display process
in production. A Boogie Board at 8.5 inches retails around $30, so film-level COGS sits
near $6 to $9 for that size.

The product: a physical board you write on with a stylus, holding the image at zero power.
An EMR digitiser layer underneath captures the strokes and pushes them to the app. The
zoom lives entirely in software. The board itself is analogue and dumb.

**Why I do not lean here.** The digitiser layer costs more than the film and pushes an A4
build to $22 to $28. Cholesteric contrast is grey on grey, well short of paper. And the
erase is all-or-nothing, so the board cannot render anything the software decides. You get
a capture device, and the display half of the promise disappears.

---

## 5. Where I land

Option A, at 2.9 inches, at 10k units, priced as a system rather than a device.

The thing worth testing before spending anything on tooling: put six mock tiles on a wall,
mount printed cards in them, and see whether anyone in the office looks at them twice in
a fortnight. The panel cost curve is solvable with volume. Whether an ambient wall changes
anyone's behaviour is the question that kills the product, and it costs $40 of foam board
to answer.

---

## Sources

- E Ink Holdings FY2026 Q2 earnings, gross margin guidance 55 to 59 percent:
  https://finance.biggo.com/news/TW_8069.TW_2026-08-13
- E Ink official shop, Spectra 6 pricing at 13.3" and 25.3": https://shopkits.eink.com/
- Large-format e-paper size ladder and yield economics, module as 70 to 75 percent of frame BOM:
  https://www.einksmart.com/en/blog/insights/large-e-ink-displays-compared.html
- Waveshare e-paper module retail pricing: https://www.waveshare.com/epaper
- E-paper refresh rate, ghosting and partial refresh limits: https://orientdisplay.com/why-does-e-ink-refresh-slowly/
- TRMNL B2B volume pricing sheet: https://trmnl.com/b2b/pricing-sheet
- Vestaboard Note pricing change, 1 September 2026: https://www.vestaboard.com/news/vestaboard-note-price-increases
- ESL unit pricing by size: https://koronapos.com/blog/how-much-do-electronic-shelf-labels-cost/
- Kent Displays Reflex cholesteric roll-to-roll process: https://kentdisplays.com/boogie-board-lcd-writing-tablet/
- Ynvisible printed electrochromic, low-cost roll-to-roll comparison: https://www.ynvisible.com/e-paper-displays/
