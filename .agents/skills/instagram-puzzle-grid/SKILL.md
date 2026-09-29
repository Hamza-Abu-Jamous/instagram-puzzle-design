---
name: instagram-puzzle-grid
description: >-
  Use this skill when the user asks to design, generate, or slice an Instagram
  Puzzle Grid (seamless grid / بازل إنستغرام). Covers the correct canvas
  dimensions (Master Canvas), the Horizontal Tangent Rule to prevent line-break
  artifacts at slice borders, safe zones for 1:1 profile cropping, the correct
  publishing order, AI image prompts, SVG Bezier laser paths, and the
  Programmers IT brand system (colors + fonts).
---

# Instagram Puzzle Grid — Engineering Skill
### Programmers IT · Devoteam Formula

> [!IMPORTANT]
> Always read this skill before generating or slicing any Instagram puzzle grid.
> It contains the exact pixel values and rules derived from real production work.

---

## 1. Master Canvas Dimensions (The Golden Formula)

Instagram displays individual posts at **4:5 Portrait — 1080 × 1350 px**.
Build the master canvas in exact multiples:

| Grid Type | Posts | Master Canvas | Each Post (after slice) |
| :--- | :---: | :---: | :---: |
| 1 row (3 posts) | 3 | **3240 × 1350 px** | 1080 × 1350 px |
| 2 rows (6 posts) | 6 | **3240 × 2700 px** | 1080 × 1350 px |
| 3 rows (9 posts) | 9 | **3240 × 4050 px** | 1080 × 1350 px |

**Width formula:** `1080 × number_of_columns` (always 3 columns)  
**Height formula:** `1350 × number_of_rows`

---

## 2. The Horizontal Tangent Rule (Zero-Slope Rule)

> [!CAUTION]
> This is the most critical rule. Violating it causes visible line breaks / steps
> at slice borders even when the design looks correct on the full canvas.

**Why does the line break at slice borders?**  
Instagram adds a 1–3 px white gap between posts. A diagonal line passing through
this gap loses part of its slope, creating a vertical step (Step Discontinuity).
Sub-pixel rounding on phone screens amplifies the error further.

**The fix — at every vertical slice border (`x = 1080` and `x = 2160`):**
1. The curve slope **must be exactly horizontal** (`dy/dx = 0`).
2. Lock the `Y` value to the same constant for **at least 40 px** before and
   after each slice border.
3. Keep the arc apex variance small — no more than **40–50 px** of vertical
   travel within the center post alone.

---

## 3. Safe Zones for 1:1 Profile Cropping

Instagram crops each post to a square **1080 × 1080 px** for the profile grid,
taken from the **vertical center** of the 4:5 post:

```
+-----------------------------------------------------------+  y = 0
|        Top Buffer (135 px) — CROPPED in profile view      |
+===========================================================+  y = 135
|                                                           |
|              Safe Square  1080 × 1080 px                  |
|      Place all text, cards, and logos HERE only           |
|                                                           |
+===========================================================+  y = 1215
|        Bottom Buffer (135 px) — CROPPED in profile view   |
+-----------------------------------------------------------+  y = 1350
```

**Side margins:** Keep all text/logos **≥ 100 px** away from the left and right
edges of each post to avoid overlap with the slice line.

---

## 4. Publishing Order (Reverse Chronological)

> [!CAUTION]
> Instagram pushes new posts to the **right**, filling the grid from bottom-left
> to top-right. Publishing in the wrong order **mirrors the entire puzzle.**

### 3-post grid (1 row) — publish in this sequence:
1. **Publish 1st** → Right post (`x: 2160–3240`)
2. **Publish 2nd** → Center post (`x: 1080–2160`)
3. **Publish 3rd** → Left post (`x: 0–1080`)

### 6-post grid (2 rows) — publish bottom row first:
1. Bottom-right post
2. Bottom-center post
3. Bottom-left post
4. Top-right post
5. Top-center post
6. Top-left post

---

## 5. Slicing Logic (Pixel-Exact Crop Coordinates)

### 3-post grid slices from a `3240 × 1350` master:

| Post | Label | Crop X | Crop Y | Width | Height |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Right (publish 1st) | POST_1 | 2160 | 0 | 1080 | 1350 |
| Center (publish 2nd) | POST_2 | 1080 | 0 | 1080 | 1350 |
| Left (publish 3rd) | POST_3 | 0 | 0 | 1080 | 1350 |

### 6-post grid slices from a `3240 × 2700` master:

| Post | Row | Crop X | Crop Y | Width | Height |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Bottom-right (1st) | Bottom | 2160 | 1350 | 1080 | 1350 |
| Bottom-center (2nd) | Bottom | 1080 | 1350 | 1080 | 1350 |
| Bottom-left (3rd) | Bottom | 0 | 1350 | 1080 | 1350 |
| Top-right (4th) | Top | 2160 | 0 | 1080 | 1350 |
| Top-center (5th) | Top | 1080 | 0 | 1080 | 1350 |
| Top-left (6th) | Top | 0 | 0 | 1080 | 1350 |

---

## 6. SVG Bezier Laser Path (Mathematically Correct)

This path passes through all three posts with **horizontal tangents at both
slice borders** (`x = 1080, y = 480` and `x = 2160, y = 480`):

```xml
<svg viewBox="0 0 3240 1350" fill="none" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <!-- Emerald gradient -->
    <linearGradient id="ribbonGrad" x1="0%" y1="50%" x2="100%" y2="50%">
      <stop offset="0%"   stop-color="#10b981" stop-opacity="0.85" />
      <stop offset="30%"  stop-color="#34d399" stop-opacity="0.95" />
      <stop offset="50%"  stop-color="#06b6d4" stop-opacity="1.0"  />
      <stop offset="70%"  stop-color="#34d399" stop-opacity="0.95" />
      <stop offset="100%" stop-color="#10b981" stop-opacity="0.85" />
    </linearGradient>

    <!-- Soft glow filter -->
    <filter id="laserGlow" x="-20%" y="-20%" width="140%" height="140%">
      <feGaussianBlur stdDeviation="12" result="blur" />
      <feMerge>
        <feMergeNode in="blur" />
        <feMergeNode in="SourceGraphic" />
      </feMerge>
    </filter>
  </defs>

  <!--
    Slice border 1: x=1080, y=480 → horizontal tangent → control points at x=780 and x=1320
    Slice border 2: x=2160, y=480 → horizontal tangent → control points at x=1920 and x=2460
    Apex: x=1620, y=440 (only 40px above border crossing)
  -->

  <!-- Glow halo -->
  <path d="M 180 720 C 480 720, 780 480, 1080 480
           C 1320 480, 1480 440, 1620 440
           C 1760 440, 1920 480, 2160 480
           C 2460 480, 2760 720, 3060 720"
        stroke="url(#ribbonGrad)" stroke-width="46" fill="none"
        opacity="0.32" filter="url(#laserGlow)" />

  <!-- Core laser line -->
  <path d="M 180 720 C 480 720, 780 480, 1080 480
           C 1320 480, 1480 440, 1620 440
           C 1760 440, 1920 480, 2160 480
           C 2460 480, 2760 720, 3060 720"
        stroke="url(#ribbonGrad)" stroke-width="7" fill="none"
        filter="url(#laserGlow)" />

  <!-- White hot core -->
  <path d="M 180 720 C 480 720, 780 480, 1080 480
           C 1320 480, 1480 440, 1620 440
           C 1760 440, 1920 480, 2160 480
           C 2460 480, 2760 720, 3060 720"
        stroke="#ffffff" stroke-width="2.4" fill="none" opacity="0.95" />
</svg>
```

---

## 7. AI Image Generation Prompts

Use with **Midjourney v6**, **Stable Diffusion**, or **Gemini Imagen**:

### Modern Tech / Luminous Cityscape
```
Ultra-wide panoramic architectural cityscape of Dubai downtown skyline,
Burj Khalifa centered, daylight golden hour transitions into modern dusk,
bright luminous sky, crystal-clear glass facade reflections, highways and
curved overpasses below, high-tech corporate atmosphere, modern corporate
lighting, clean atmosphere without heavy fog, shot on Phase One 150MP
medium format, pristine sharpness, hyper-realistic, high contrast, clean
architecture photography, architectural digest grade --ar 24:10 --stylize 250 --v 6.0
```

### Platinum White / Minimalist Corporate
```
Ultra-wide panoramic modern architectural masterview, Dubai DIFC future
architecture, pristine white concrete, luminous daylight, clear bright sky,
soft reflective glass surfaces, ultra-minimalist tech campus vibe, emerald
green accent lighting glowing subtly, clean airy spacious composition with
vast negative space, premium corporate headquarters, architectural render
style, 8k resolution, photorealistic, pristine daylight clarity --ar 24:10 --v 6.0
```

---

## 8. Brand System — Programmers IT

### Colors
| Token | Hex | Usage |
| :--- | :--- | :--- |
| Neon Emerald (primary) | `#10b981` | Tech accent, AI motif |
| Deep Emerald | `#059669` / `#047857` | Headlines, bold text |
| Cyan Accent | `#06b6d4` | Gradients, glow points |
| Deep Navy (dark bg) | `#0b1120` + `#0f172a` | Dark-theme backgrounds |
| Clean Platinum (light bg) | `#f8fafc` | Light-theme backgrounds |

### Typography
| Use | Font | Weight |
| :--- | :--- | :--- |
| Arabic headlines | **Cairo** | 900 (Black), 800 (ExtraBold) |
| English headlines & icons | **Plus Jakarta Sans** | 800 (ExtraBold), 700 (Bold) |

---

## 9. Quick Checklist Before Generating

- [ ] Master canvas is an exact multiple of `1080 × 1350`
- [ ] Curve has horizontal tangent (`dy/dx = 0`) at `x = 1080` and `x = 2160`
- [ ] Y locked constant for ≥ 40 px on both sides of each slice border
- [ ] All text/logos inside the safe square (`y = 135` to `y = 1215`)
- [ ] Side margins ≥ 100 px from slice borders
- [ ] Publishing order is Right → Center → Left (bottom row first for 6-post)
