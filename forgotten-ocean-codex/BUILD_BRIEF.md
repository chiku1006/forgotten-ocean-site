# FORGOTTEN OCEAN — Codex Master Build Brief

You are the lead creative technologist, Three.js/WebGL engineer, technical artist, interaction designer, and performance engineer. Implement a real, functioning, visually compelling 3D portfolio in this repository. **Do not stop at a plan, README, mockup, screenshot-only hero, static background image, or simplistic prototype.** Actively build and test the site.

## 0. CRITICAL FIRST STEPS
1. Inspect the actual repository: package.json, entry points, source tree, installed rendering/animation libraries, assets, Git state, routes, runtime, existing scroll/camera controls. Identify what is genuinely implemented rather than trusting README claims.
2. Determine if the current repo is suitable to refactor. If it is an Igloo rebuild, preserve and adapt only genuinely working pieces (camera timeline, render loop, input handling, transitions, reusable shaders). Avoid unnecessary wholesale rewrites. If the repo is unsuitable, explain why in a short plan and create a clean implementation in a separate branch.
3. Protect user work: never overwrite existing content blindly; create a Git checkpoint/branch before substantial edits. DO NOT deploy, push or modify Cloudflare/Vercel production without explicit permission.
4. Open and examine all supplied reference images and both live references using browser tools if available. If no browser is available, proceed from references and state the verification limitation. Reference sites: https://www.igloo.inc/ and https://activetheory.net/ . Study the experience principles, not their proprietary code or assets.
5. Read `references/01-full-experience-storyboard.png` first. It is the **authoritative visual/storyboarding guide**. Other images are supporting inspiration, not alternate themes.

## 1. PRODUCT VISION — NON-NEGOTIABLE
Create a premium, natural, atmospheric underwater portfolio named **FORGOTTEN OCEAN**, authored for a visual storyteller / video editor / motion graphics artist. The experience combines the scroll-driven exploratory composition and object selection of Igloo with the highly polished cinematic world-building of Active Theory, but ALL actual visuals, copy, geometries, animations and interactions must be original.

**Mood:** mysterious, serene, awe-inspiring, photorealistic/stylized-real rather than fantasy neon. Deep teal ocean water, filtered sunbeams, naturally moving sea life, huge weathered ancient submerged ruins, irregular stones, algae, kelp, corals, drifting sediment, faint underwater caustics. A whale far in the distance during the intro is a powerful silhouette, not a constant particle-intensive animated centerpiece.

**Explicitly avoid:** sci-fi reactors, futuristic circuitry, neon energy cores, holographic HUDs, glowing UFO portals, glassmorphism SaaS cards, generic tailwind template sections, random bright gradients, huge bloom, fake 3D created by stacking static images, jarring cut transitions. Subtle bioluminescence allowed only as an environmental detail. Do not claim the sample images are the actual website.

Brand: small `CHIKU.` logo at the top-left; calm editorial typography (one tasteful display sans with a compact mono for tiny annotations). Minimal edge-aligned UI, subtle scroll progress indicator and sound toggle. Use accessible contrast; avoid placing too much text directly over busy reef geometry.

## 2. REQUIRED EXPERIENCE MAP — FULL 9-SCENE STORYBOARD
Treat all 9 scenes as a connected real-time world, not 9 disconnected pages.

1. **ENTRY / HERO:** First entry begins looking upward through blue-green water. Filtered rays reveal a distant whale silhouette crossing slowly above a rocky coral foreground. `CHIKU.`, short hero copy such as `A Visual Storyteller.`, subtle `SCROLL TO EXPLORE`. Intro takes seconds only once; user can skip. No fabricated personal claims. Scroll starts a cinematic descent.
2. **APPROACH THE RUINS:** Camera glides forward/down along an intentional spline between coral-covered ancient pillars, rock arches, kelp and schooling fish. Strong spatial depth, occlusion, parallax. Natural temple architecture forms the main scene landmark.
3. **CHOOSE A PATH:** Camera arrives at two distinct, giant ancient weathered stone artifacts/pillars in-world, visibly titled `WORK` and `INFO`, with small tasteful icons/annotations. They are actual 3D raycast targets with pointer hover, keyboard focus equivalent, screen-reader-accessible HTML navigation alternative and robust click/tap targets. No project cards revealed here. Scroll can progress past the scene; clicking either opens a portal.
4. **ENTER WORK — CINEMATIC TRANSITION:** On WORK selection, pause/lock the main scroll timeline, preserve its current position, smoothly animate camera along a safe spline through the stone arch. Add restrained caustic refraction, light occlusion, drifting sediment and fast-but-readable easing. No sudden teleport, white flash or generic fade-to-black. Transition must be reversible and support Back/Escape.
5. **WORK — IMMERSIVE VIDEO GALLERY:** A distinctive submerged gallery built into the ancient architecture, with 3D-framed project surfaces integrated into rocks/ruins, not generic floating rectangles. Show user's actual videos where provided. Implement data-driven project manifest (`src/data/projects.*` or equivalent) with title, category, role, year (only if known), video, optimized poster, description, links. If real assets are absent, use visually cohesive clearly labeled placeholder assets without inventing projects, clients, awards, dates or biographies. Categories: ALL / EDITS / MOTION / 3D / SHORTS. Animated filtering, spatial camera movement between featured project surfaces, hover focus/tilt, and click-through to a sophisticated project-detail experience with video player and next/previous navigation. All controls keyboard operable. Loading video must not block the 3D scene. Back leads seamlessly to the fork in the ocean.
6. **ENTER INFO — DIFFERENT CINEMATIC TRANSITION:** INFO object feels distinct from WORK. On click, camera curves around weathered ancient columns and crosses a natural stone ring, with flowing kelp and subtle silt displacement. DO NOT simply reuse the exact WORK transition.
7. **INFO — ABOUT ME:** Discover a monumental, moss-covered sculptural stone face or carved artifact in the temple ruins. Calm editorial text tells the portfolio owner's story. Headings and placeholders for About Me, video editing, motion graphics, 3D/VFX, process, services, tools. Do NOT invent background, achievements, age, location, client list or experience. Content must be editable in `src/data/site.*`. Provide tasteful animations tied to camera progress. Have accessible plain-HTML fallback.
8. **CONNECT:** Camera emerges into a breathtaking ocean clearing. Instagram, Fiverr, WhatsApp must be visibly available as real, accessible link elements integrated into this scene; the URLs must be configurable placeholders until the user provides actual addresses. Ensure safe outbound links with `rel="noopener noreferrer"` for new tabs. Contact UI remains usable independent of WebGL.
9. **SEAMLESS LOOP:** Keep scrolling from CONNECT and smoothly merge into the original opening environment. The sea floor, camera orientation, fog, ambient creatures and light should visually mask the wrap. No scroll snap to top, apparent reload, black frame, camera pop, duplicated intro preloader or sound restart. Reverse scrolling must feel coherent. If a mathematically perfect seamless loop would compromise input stability, deliver a polished and measurable illusion with a visually hidden wrap and document it.

Main state machine: `MAIN_WORLD`, `ENTERING_WORK`, `WORK`, `LEAVING_WORK`, `ENTERING_INFO`, `INFO`, `LEAVING_INFO`. Guard against duplicate transitions and race conditions. URL hash or route state should deep-link and support browser back/forward where feasible. After modal / project close, restore prior point and scroll/camera continuity. Input works with mouse wheel, touch, trackpad, keyboard, resize, tab switching.

## 3. VISUAL DIRECTION & ASSET PRODUCTION
- Follow `references/01-full-experience-storyboard.png`: 3x3 reference with whale entrance, stone ruins, WORK / INFO pillars, distinct entrance animations, integrated gallery, About Me, social links, loop return.
- `references/02-igloo-style-interaction.png`: only for cinematic center object / small technical annotations / click-to-explore principles, NOT snowy terrain or visual cloning.
- `references/03-natural-underwater-ruins.png`: natural stone arch, corals, monument silhouette, rays and underwater spatial proportions. Avoid any glowy portal ring shown in inspiration; make light physics environmental and grounded.
- `references/04-lighting-atmosphere.png`: lighting/material palette only. No glass biodome in final design.
- Use real low-/mid-poly optimized 3D structures/models with art-directed geometry. Handcrafted geometry and approved CC0/clearly licensed assets are acceptable; document origin, attribution and licenses. Do not scrape or copy proprietary production assets from reference websites. If external asset downloads aren't possible, create credible original procedural meshes, vertex color/textured rock with noise, instanced corals/kelp, and placeholder assets prepared for swapping.
- Use convincing but efficient lighting: baked or faked shadowing, graded fog, efficient sunlight shafts, caustic shader or lightweight decal. Reference target is **visual quality**, not literally reproduce high-cost film effects in real-time.
- Implement responsive desktop framing first, then deliberate mobile composition, smaller particle budgets, optional static/2D fallback. Preserve content/accessibility if WebGL2 unavailable or user requests reduced motion.

## 4. ENGINEERING PRINCIPLES
- Prefer the existing project's Three.js/Svelte/React/GSAP stack where it is stable. Introduce dependencies only if justified. Make one coherent renderer and a single centralized world timeline rather than multiple disconnected requestAnimationFrame loops.
- Main scroll should map to one normalized progress value; do not force integer chapter snaps or absorb scroll in a dead zone. Use fixed, tunable damping; preserve responsiveness even for small wheel deltas. Reconcile wheel, touch, keyboard, trackpad and reverse scrolling.
- Separate camera pose calculation, physics/scene animation, user interactions and rendering. Frame-time hot path should be allocation-light. Disable or throttle expensive postprocessing. Avoid excessive transparency, shadow map updates, full-screen per-pixel shaders and per-fish draw calls. Use batching/instancing, geometry LOD, compressed KTX2 textures, glTF/GLB/Draco/Meshopt where practical, and asset streaming.
- Pause or cap idle renders when world is stationary, respecting moving fish/ambient atmosphere only when visible; pause offscreen/in hidden tabs.
- Load hero quickly (small initial assets), stream later scenes and project posters before needed, defer videos until selected. Aborted/failed downloads should not freeze scene or block the rest. Release GPU memory and textures when no longer used. Plan for WebGL context loss and recovery.
- Optional soundscape initially muted or opt-in; sound toggle remembers user choice during session; no unavoidable autoplay. Gracefully handle restricted audio contexts.
- Main navigation links and content must remain usable without WebGL; provide a fallback that represents the actual content, not a blank canvas.

## 5. MEASURABLE PERFORMANCE — DO NOT CLAIM UNTESTED 120 FPS
Target machine for desktop verification: Windows 11, i5-14400F, RTX 4060, 32 GB RAM, browser with hardware acceleration enabled. Also test integrated/software rendering or reduced quality if available.
- At 60 Hz, aim for ~60 fps during normal movement; report P50/P95/P99 frame times, not just average FPS. Baseline targets after shader warmup: P95 <= 16.7ms, P99 <= 33.3ms on target desktop under representative scenes. Treat as goals, not a claim of guaranteed result.
- No >100ms input-to-first-visible-camera-response on small wheel movements. Aim <50ms at P95 for camera response in normal warmed state if feasible; explicitly measure from wheel event to first measurable camera pose/draw.
- Track input-to-camera response, draw calls, triangles, texture use, GPU/CPU time where tools permit, WebGL context loss, navigation and transition long tasks, memory growth after repeated portal open/close and loop wrap.
- Add reproducible automated browser tests (Playwright if available): scroll down, reverse scroll, tiny wheel inputs, rapid wheel jumps, repeated portal entry/exit, click project, browser back, loop wrapping twice, mobile, reduced motion, WebGL unavailable, missing image/video assets, context loss/recovery.
- Ensure build and lint/typecheck pass. Run test loops repeatedly at local **production build**, not just Vite dev mode. Compare screenshots to reference storyboard at known camera progress values; note that reference render is conceptual and may not be visually achievable without real authored assets.
- If targets fail, profile and iterate; show observed numbers, likely cause and specific trade-off. Never quietly downgrade entire site to a bland 2D page or falsely label it smooth.

## 6. IMPLEMENTATION PHASES — BUILD, DON'T JUST PLAN
Create a brief plan, then execute the work in real code. Commit coherent changes at meaningful milestones.

**Milestone A — Foundation:** audit, save existing state, create asset/data manifests, establish camera path/world scale, baseline performance test and baseline screenshot.

**Milestone B — Hero and world:** make a visually strong full-viewport original ocean scene with whale silhouette, natural seabed, ruins, useful UI and continuous responsive camera journey. Complete first 3 scenes; inspect screenshots against storyboard.

**Milestone C — WORK and INFO:** actual interactive 3D pillars, camera-enter animations, functional gallery with filters, video playback/project detail, real About page integration, exit/back behavior.

**Milestone D — Connect + infinite loop:** Instagram/Fiverr/WhatsApp contact section, natural camera closing composition, correct seamless wrap and reverse scroll, social placeholders.

**Milestone E — Polish and performance:** asset quality, typography, responsive layouts, visual QA, automated edge-case tests and instrumentation, production build; fix failing frame-time and input-latency cases where possible.

Build as far as real constraints allow, but do not call a flat placeholder site finished. Maintain a clearly stated checklist of completed/partial/unimplemented requirements. Favor fully functioning high-quality sections over many fake scenes. Avoid asking the user questions that can be answered by inspecting files; use editable placeholders for missing copy, personal links and project videos.

## 7. FINAL DELIVERABLE AND REPORT
At the end provide: local running URL, actual changed files, branch/commit(s), any asset license notes, exactly what scenes/interactions work, screenshots of hero / WORK+INFO fork / projects / info / contact / loop, production build results, verified browser tests, performance numbers with test conditions and known gaps. **Never deploy to Cloudflare, GitHub Pages or Vercel without explicit consent.** Do not imply visual similarity/FPS targets are achieved without screenshots and numbers.

Start by auditing this repository and the references, then implement the first fully working visual milestone immediately. The priority order is **visual fidelity > reliable interaction > truthful measurable smoothness**, balanced so no one area completely fails. The final intended website must satisfy all three.
