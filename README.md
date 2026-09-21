# Tetra PRO — 3D hero section

A scroll-driven hero section for the DEKA Tetra PRO fractional CO₂ laser, built with
Three.js and GSAP ScrollTrigger. It runs as a single self-contained HTML block that can
be pasted into WordPress (Custom HTML block or Elementor HTML widget).

## Files

| File | What it is |
| --- | --- |
| `tetra-pro-hero-wordpress-build.html` | The hero. Paste the whole file into one HTML block in a full-width section with no padding. |
| `assets/Tetra Pro 3D Model.glb` | The 3D model of the machine (12 MB). |
| `assets/Logo.png` | Tetra PRO logo, shown on the loading screen. |

## Setup

1. Upload the `.glb` and the logo to the WordPress Media Library. WordPress blocks `.glb`
   by default — a plugin such as *File Upload Types* allows it.
2. Open the HTML file and put your Media Library URLs into the config block at the top:

   ```js
   window.TETRA_HERO = {
     model: "https://…/Tetra_Pro-v1.glb",
     logo:  "https://…/Logo.png",
     scrub: 0.9,      // seconds the animation takes to catch up with the scroll
     normalize: true  // smoother touch scrolling on phones and tablets
   };
   ```
3. Paste the file into the HTML block and publish.

## How the animation is timed

The hero is pinned while five chapters play. Each chapter holds for 12% of the scroll and
each transition between chapters takes 8%, so the same swipe always advances the animation
by the same amount.

| Scroll | Chapter |
| --- | --- |
| 0 – 16% | Build-up: the machine assembles from a blue blueprint, driven by your scroll |
| 0 – 14% | 00 — Intro |
| 20 – 34% | 01 — The system, with labelled parts |
| 40 – 54% | 02 — DOT Therapy close-up |
| 60 – 74% | 03 — CoolPeel |
| 80 – 100% | 04 — Closing |

`BUILD_END` near the keyframe list controls how much scroll the build-up takes.

## Notes

- Three.js and GSAP load from cdnjs; nothing is bundled.
- The model is 12 MB, which dominates the first load. Compressing it with
  [gltf.report](https://gltf.report) usually brings it to 2–4 MB — export as **GLB**, and
  avoid Draco or Meshopt compression unless the decoder is added to the page.
- Visitors with "reduce motion" enabled get the finished machine without the animation.
