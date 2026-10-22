# UI/UX, VFX and SFX/Audio production for Roblox (as of Oct 2026)

Method note: create.roblox.com could not be reached from this environment (the proxy blocked it). Official doc text was therefore read from Roblox's own docs source repo, github.com/Roblox/creator-docs, at its latest commit (21 Oct 2026). Each create.roblox.com/docs URL below is the published page built from that source file. DevForum and community items came through web search and are labelled as community or secondary sources. The GitHub API was blocked, so repo activity numbers (stars, last push) for the UI frameworks are not available.

## UI: layout, safe areas, mobile/console, frameworks, Figma pipeline, top-game UX patterns

### Takeaway
Build every ScreenGui mobile-first. Use Scale for position and size, AnchorPoint for alignment, and UIListLayout/flex or grid for structure. Leave ScreenInsets at its default of CoreUISafeInsets for anything a player taps. Adapt to screen size with GuiService.ViewportDisplaySize, and handle touch, gamepad and keyboard through the Input Action System. As of late 2026 Roblox also ships an engine-level styling system (StyleSheets, tokens, themes and queries) with a Style Editor that is still in beta. A small team can use it to keep UI consistent without adopting a code framework. For beginners, plain instances built in Studio (optionally imported from Figma) plus the styling system are the lowest-risk path. React-Lua, Fusion and Vide add structure but each has a learning curve.

### Cited Findings
**Layout fundamentals**
- Position and Size are UDim2 values. Scale is a percentage of the container and Offset is pixels, and the two add together. Typing a bare `0.5` in Studio is read as Scale; typing `20` is read as Offset. — [Roblox Docs: Position and size](https://create.roblox.com/docs/ui/position-and-size)
- AnchorPoint is a 0–1 fraction of the object's own size. With (0.5, 0.5), position and size changes move and scale outward from the centre. — [Roblox Docs: Position and size](https://create.roblox.com/docs/ui/position-and-size)
- Scale is the recommended unit for positioning ("pixels can vary arbitrarily by both number and density across devices") and for sizing. Roblox warns that, for example, 75% width "would render to a huge size on 4K TVs for console players," so adapt layouts to screen size. — [Roblox Docs: Cross-platform development](https://create.roblox.com/docs/projects/cross-platform)
- `GuiService.ViewportDisplaySize` returns `Enum.DisplaySize` Small/Medium/Large so UI can adapt without guessing from pixel counts. Style Queries in the Style Editor can switch styles on ViewportDisplaySize and `UserInputService.PreferredInput`. — [Roblox Docs: Cross-platform development](https://create.roblox.com/docs/projects/cross-platform)
- UIListLayout supports flex behaviour, including `Wraps` so children flow onto a new line when they overflow. Grid and table layouts have their own doc pages. — [Roblox Docs: List and flex layouts](https://create.roblox.com/docs/ui/list-flex-layouts); [Grid and table layouts](https://create.roblox.com/docs/ui/grid-table-layouts)
- Size modifiers (UIAspectRatioConstraint, UISizeConstraint, UITextSizeConstraint) are documented together. With TextScaled on, text scales with its container and respects those constraints. — [Roblox Docs: Size modifiers](https://create.roblox.com/docs/ui/size-modifiers)
- 9-slice uses the `SliceCenter` property, set through an in-Studio editor, so a single small image can stretch into panels and buttons of any size without distorting the corners. — [Roblox Docs: 9-slice](https://create.roblox.com/docs/ui/9-slice)

**Safe areas and notches (ScreenInsets)**
- `ScreenGui.ScreenInsets` has four options:
  - **CoreUISafeInsets** (default) keeps UI clear of the Roblox top-bar buttons and device cutouts. It is "recommended if the ScreenGui contains interactive UI elements".
  - **DeviceSafeInsets** avoids notches and cutouts only, not the top bar.
  - **TopbarSafeInsets** places UI between the top-bar controls and the right edge, flexing horizontally with the top bar's content.
  - **None** should be used only for non-interactive content such as background images.

  — [Roblox Docs: On-screen containers (ScreenInsets include)](https://create.roblox.com/docs/ui/on-screen-containers)
- Cross-platform checklist: every button or control should be reachable and "not blocked or obscured by device cutouts or Roblox UI elements". — [Roblox Docs: Cross-platform development](https://create.roblox.com/docs/projects/cross-platform)
- Where Roblox's own mobile buttons sit depends on device orientation and whether the device has a virtual nav bar or a physical home button, as documented in a table on the mobile input page. — [Roblox Docs: Mobile input](https://create.roblox.com/docs/input/mobile)

**Input: touch, gamepad, keyboard**
- Roblox recommends the **Input Action System** to support all input types: InputContext → InputAction → InputBinding. Each action gets one binding per device, e.g. LeftShift, ButtonY, and a touch binding linked through `InputBinding.UIButton` to an on-screen button. — [Roblox Docs: Input Action System](https://create.roblox.com/docs/input/input-action-system)
- `InputAction.PreferredBinding` and `UserInputService.PreferredInput` report the player's current primary input. `InputActionLabel` gives no-code button-prompt hints that update when the player switches device. `GetImageForKeyCode()` returns Xbox or PlayStation glyphs. — [Roblox Docs: Cross-platform development](https://create.roblox.com/docs/projects/cross-platform)
- Haptics are supported through `HapticEffect` instances, with types such as `UIClick` and `GameplayCollision`, on most iPhone, Pixel and Galaxy devices. — [Roblox Docs: Mobile input](https://create.roblox.com/docs/input/mobile)
- Roblox runs an "Interactivity Showcase" place that demonstrates its cross-platform UI patterns. — [Roblox Docs: Cross-platform development](https://create.roblox.com/docs/projects/cross-platform)

**Styling system (new since 2025; still beta)**
- UI styling is Roblox's CSS-like system:
  - `StyleSheet` holds `StyleRule`s whose selectors match by class, tag, name, modifiers (UICorner/UIStroke) or GuiState (e.g. Hover).
  - **Tokens** are variables such as a shared colour.
  - **Themes** are swappable token sets, e.g. light and dark.
  - **Queries** apply styles by screen size, input type or accessibility setting.
  - `StyleLink` attaches one StyleSheet to a ScreenGui tree.

  It is "the foundation for the Style Editor and the end-to-end token pipeline". — [Roblox Docs: UI styling](https://create.roblox.com/docs/ui/styling)
- The Style Editor page still carries a beta alert. — [Roblox Docs: Style Editor](https://create.roblox.com/docs/ui/styling/editor)
- Built-in queries include `@ReducedMotionEnabledTrue`, which maps to `GuiService.ReducedMotionEnabled`, and ViewportDisplaySize states. — [Roblox Docs: CSS comparisons](https://create.roblox.com/docs/ui/styling/css-comparisons)

**UI frameworks**
- React Luau (roblox/react-lua): "A comprehensive, but not exhaustive, translation of ReactJS 17.x into Luau". It is MIT-licensed and distributed on the Creator Store and Wally, with docs at react-luau.dev. — [GitHub: Roblox/react-lua README](https://github.com/Roblox/react-lua)
- Community view of React-Lua: good for "large/complex/dynamic UIs" but with a "relatively steep learning curve". Some developers say frameworks are unnecessary for simple games. This is opinion. — [DevForum: How To: React + Roblox](https://devforum.roblox.com/t/how-to-react-roblox/2964543?page=2); [DevForum: Question for react-lua users](https://devforum.roblox.com/t/question-for-react-lua-users/3709550)
- Fusion (dphfox, formerly elttob) describes itself as a "portable Luau companion library for simpler, more descriptive code". It is MIT-licensed, has "batteries-included configuration for Roblox", and offers an "on-rails tutorial". — [GitHub: dphfox/Fusion README](https://github.com/dphfox/Fusion); [Fusion docs](https://elttob.uk/Fusion/latest/tutorials)
- Vide (centau) is a "reactive Luau UI library inspired by Solid": fully typecheckable, declarative and concise, with a crash-course tutorial and a roblox-ts JSX variant. — [GitHub: centau/vide README](https://github.com/centau/vide); [@rbxts/vide README](https://cdn.jsdelivr.net/npm/@rbxts/vide@0.6.1/README.md)
- Roact is the older predecessor. A community comparison says React-Lua is "almost 1:1" with React, whereas Roact had deviations and performance issues. Treat Roact as **outdated** for new projects. — [DevForum: How To: React + Roblox](https://devforum.roblox.com/t/how-to-react-roblox/2964543?page=2)

**Figma → Roblox pipeline (community tools, mid-2026)**
- UILint v2 is a Figma plugin with a Studio companion. It exports the layer hierarchy and images and rebuilds them as Roblox instances. The free tier covers local linting and manual export; Smart Sync and Smart Scale are paid. — [DevForum: UILint v2](https://devforum.roblox.com/t/plugin-uilint-v2-import-figma-ui-into-roblox-studio/4765869)
- RoImport is a free Figma plugin with a Roblox plugin. Layer-naming tags (_Image, _Button, etc.) control the output, and it exports auto-layouts. — [DevForum: RoImport](https://devforum.roblox.com/t/free-figma-to-roblox-plugin-roimport/4731967)
- Other tools: Figma Importer Assistant (free), GuiForge (a browser editor that outputs Luau or .rbxmx), UI Designer Pro, and FigBloxUI. — [DevForum: Figma Importer Assistant](https://devforum.roblox.com/t/2961561); [DevForum: GuiForge](https://devforum.roblox.com/t/guiforge-roblox-ui-editorfigma-export/4834077); [DevForum: UI Designer Pro](https://devforum.roblox.com/t/plugin-ui-designer-pro/4685902); [DevForum figma tag](https://devforum.roblox.com/tag/figma)
- Common pain point: imports often come out in Offset (pixels) and need converting to Scale, plus constraints, before they work on mobile. — [DevForum: Importing UI From Figma SUCKS](https://devforum.roblox.com/t/importing-ui-from-figma-sucks/3381689)

**Images, moderation and privacy**
- Asset Privacy sets the default privacy for newly created **Images, Decals and Meshes** only. Your own assets always work in your own games, and permission can be granted to collaborators or other games. — [Roblox Docs: Asset privacy](https://create.roblox.com/docs/projects/assets/privacy)
- Image resolution cap: 1024×1024 is the figure widely cited by the community, but I found only low-quality secondary sources and they conflict. One claims "no strict limit", and file-size claims range from 1 MB to 20 MB. — [noping.com blog](https://noping.com/blog/how-to-upload-multiple-decals-at-once-in-roblox) (unverified)
- Supporting evidence from the official particle docs: they use a 1024×1024 sheet as their example 8×8 flipbook. — [Roblox Docs: Particle emitters](https://create.roblox.com/docs/effects/particle-emitters)

**UX patterns (official game-design guidance, with top-game examples)**
- Five UI principles: Prioritization (a "hierarchy of information", contextual buttons), Attention (colour, size, space, proximity, movement, "in moderation"), Visual language (written up as a style guide), Conventions, and Consistency.
  - The X close button sits top-right.
  - Grey means unusable and a lock icon means not yet unlocked.
  - Prices you can't afford show in red.

  — [Roblox Docs: UI and UX design](https://create.roblox.com/docs/production/game-design/ui-ux-design)
- Top-game examples cited:
  - Super Striker League swaps the Sprint/Tackle buttons for Deke/Pass when the player has the ball.
  - Dragon Adventures makes its best-value coin bundle larger and pads it more.
  - Jailbreak puts a gold stripe under premium season-pass rewards.
  - Berry Avenue's avatar flow is low-friction: HUD button → category tabs → instant preview → Done.

  Spellbound RPG is held up as a minimal UI suited to mobile. — [Roblox Docs: UI and UX design](https://create.roblox.com/docs/production/game-design/ui-ux-design)
- Roblox advises using **Experiments** (A/B tests) on button placement and HUD layouts, and **Configs** to toggle platform-specific or seasonal UI live. — [Roblox Docs: UI and UX design](https://create.roblox.com/docs/production/game-design/ui-ux-design)
- Onboarding (FTUE) is judged by Day-1 retention and the "player funnel". The goals are to teach the essentials, which means controls plus the core loop (what and why), and to "get to the fun quickly", because "New players typically decide their interest in a game within minutes". The levers for that are low early XP thresholds, social motivators, and starter items and currency (tested with Experiments). Players should finish wanting more: give short, mid and long-term goals and end on a designed "moment of joy". — [Roblox Docs: Onboarding](https://create.roblox.com/docs/production/game-design/onboarding)
- Onboarding techniques:
  - Visual cues: prominence, highlights, hints.
  - Contextual tutorials that trigger on the player's first interaction with a feature, which reduces cognitive load.
  - Timed hints. For example, if playtests show most players press a button within 10 seconds, highlight it at 11 seconds, show the hint only once, and only to players who are stuck.

  — [Roblox Docs: Onboarding techniques](https://create.roblox.com/docs/production/game-design/onboarding-techniques)
- Shop UX: Roblox has dedicated docs on contextual purchases, monetization foundations and season-pass design (not read in depth here). — [Roblox Docs: Contextual purchases](https://create.roblox.com/docs/production/game-design/contextual-purchases)

### Inferences
- Recommended beginner stack:
  - Build UI as Studio instances, all in Scale.
  - Add UIAspectRatioConstraint to square elements such as icons and buttons.
  - Use UIListLayout/flex or grid for lists, and 9-slice images for panels.
  - Put one StyleSheet with colour and font tokens on each ScreenGui.
  - Use the Input Action System with InputActionLabel for prompts.

  Bring in Fusion or Vide (lighter, Roblox-native reactive) or React-Lua (the largest ecosystem; Roblox uses it internally) only once UI state gets complex. Vide and Fusion are likely to suit a Luau-light team better than React's hooks and reconciler concepts.
- Since the Style Editor is still beta, build a fallback: tokens can also live in a ModuleScript.
- Test in Studio's Device Emulator on a notched phone, a tablet and a 1080p/4K "console" view, with a gamepad connected.

### Gaps
- No official minimum touch-target size in Roblox docs; I found none. (General mobile HIG figures, 44pt on iOS and 48dp on Android, are external conventions, not Roblox guidance.)
- No official image upload resolution or size limit, or monthly image upload quota, could be confirmed. The Roblox asset pages I could read do not state them.
- No repo activity or maintenance metrics for React-Lua, Fusion or Vide, because the GitHub API was blocked.
- No accuracy or price comparison of the Figma import plugins.

## VFX: particles, beams, trails, highlights, flipbook authoring, camera shake, mobile budgets, replication

### Takeaway
ParticleEmitter (with flipbooks, Squash and LightEmission), Beams, Trails and Highlights are the core toolkit. The main mobile risks are fill-rate and overdraw from large or overlapping transparent particles, and memory from many unique flipbook textures (clients automatically turn flipbooks off when low on memory). The standard architecture: the server validates and fires a small RemoteEvent, then each client spawns the effect locally. I found no official 2025–26 announcement of new ParticleEmitter features.

### Cited Findings
- A single ParticleEmitter emits at most **400 particles per second (100 per second on mobile)**. "Keep the particle rate as low as possible." — [Roblox Docs: Particle emitters](https://create.roblox.com/docs/effects/particle-emitters)
- "Particle size can impact performance due to fill-rate. The more pixels particles occupy on a player's screen, the more costly it is on the GPU." Overlapping transparent layers cause overdraw. — [Roblox Docs: Particle emitters](https://create.roblox.com/docs/effects/particle-emitters)
- Flipbook layouts are 2×2, 4×4 or 8×8 (64 frames, e.g. a 1024×1024 sheet), or Custom via FlipbookSizeX/Y. Leave transparent spacing between frames so mip filtering doesn't bleed. Modes are Loop, OneShot (frame rate follows Lifetime), PingPong and Random (crossfading). FlipbookStartRandom randomises the start frame. — [Roblox Docs: Particle emitters](https://create.roblox.com/docs/effects/particle-emitters)
- "Clients automatically deactivate flipbooks when they are low on memory, which is likely for older mobile phones." Mitigations: fewer unique animated effects, smaller textures, reused textures. — [Roblox Docs: Particle emitters](https://create.roblox.com/docs/effects/particle-emitters)
- Use .png with transparency. LightEmission 0 is normal blending and 1 is additive (glow), which also hides dark areas of grayscale textures. LightInfluence controls how much scene lighting affects the particles. — [Roblox Docs: Particle emitters](https://create.roblox.com/docs/effects/particle-emitters)
- Squash scales particles non-uniformly over their lifetime. It suits rain, where stretched default sparkles pass for raindrops. — [Roblox Docs: Particle emitters](https://create.roblox.com/docs/effects/particle-emitters)
- Highlight: the client shows at most **255 Highlights at once**; any beyond that are silently ignored. DepthMode is AlwaysOnTop or Occluded. Toggling `Enabled` has "no impact on performance". — [Roblox Docs: Highlighting](https://create.roblox.com/docs/effects/highlighting)
- A Beam draws its texture as two triangles per segment between two Attachments, and attachment orientation shapes the curve. A Trail fades its segments over Lifetime using a Transparency NumberSequence. — [Roblox Docs: Beams](https://create.roblox.com/docs/effects/beams); [Roblox Docs: Trails](https://create.roblox.com/docs/effects/trails)
- Performance guide: decals, textures and particles "don't batch well and introduce additional draw calls", and "property changes to ParticleEmitters can have a dramatic impact on performance". The scene-analysis tools break draw counts down by Particles and UI. — [Roblox Docs: Improve performance](https://create.roblox.com/docs/performance-optimization/improve); [Scene analysis](https://create.roblox.com/docs/performance-optimization/scene-analysis)
- Replication pattern (community consensus):
  - The server computes hitboxes and cooldowns, then fires clients so they create the effects.
  - Send small instructions rather than effect instances.
  - Optionally fire only to players within range.
  - Rate-limit remotes, because exploiters spamming VFX remotes can lag other clients.
  - FireAllClients does not reach players who join later, so replay any active persistent effects for new joiners.

  — [DevForum: Correct way of scripting VFX?](https://devforum.roblox.com/t/correct-way-of-scripting-vfx/2439994); [DevForum: Client-sided VFX](https://devforum.roblox.com/t/client-sided-vfx/2792835); [DevForum: preventing VFX remote spam](https://devforum.roblox.com/t/how-should-i-prevent-exploiters-spamming-my-remoteevent-for-vfx-replication/4749010); [DevForum: late joiner replication](https://devforum.roblox.com/t/2323228)
- 2025–26 features: no official new-ParticleEmitter announcement turned up. Long-standing community requests (burst emission, collision, sub-emitters) are still being met by community modules such as "Particle Emitter +" and a "3D Particle Creator" module from April 2026. — [DevForum: VFX system update features (request)](https://devforum.roblox.com/t/vfx-system-update-features/1293316); [DevForum: Particle Emitter +](https://devforum.roblox.com/t/particle-emitter/1900792); [DevForum particle tag](https://devforum.roblox.com/tag/particle)
- Roblox's artist curriculum covers particle emitters, beams, trails, flipbooks and light sources. — [Roblox Docs: Work with particle emitters (curriculum)](https://create.roblox.com/docs/tutorials/curriculums/artist/work-with-particle-emitters)
- Camera shake: there is no official Roblox tutorial. The general technique is to add a small offset (here, to Camera.CFrame) and ease it back to zero with an out-cubic curve. Keep shake small because big shake causes nausea. For heavy hits, a hit-stop of about 50–100 ms is suggested. These are non-Roblox game-feel sources. — [Medium: Practical juicing](https://medium.com/@dvdfu/practical-juicing-for-game-devs-efe9b06c246b); [Wayline: Game feel lesson](https://www.wayline.io/learn/game-feel/1)

### Inferences
- Mobile VFX budget rules of thumb, derived from the docs above:
  - Use bursts (`:Emit(n)`) rather than high continuous Rate.
  - Keep particles small on screen and avoid stacking many additive layers.
  - Share a few flipbook sheets across effects; consider 512×512 4×4 sheets.
  - Pool or disable emitters instead of changing many properties every frame.
  - Gate shake and flashes behind ReducedMotionEnabled.
- Flipbook authoring: render a frame sequence in EmberGen, Blender or After Effects, pack it into a power-of-two grid sheet with padding (e.g. TexturePacker or Photoshop), and upload it as an image. No official Roblox doc names specific DCC tools for this.

### Gaps
- No confirmed list of 2025–26 VFX engine features, and no official ParticleEmitter roadmap found.
- No official numeric particle budget per scene for mobile; only the per-emitter rate cap.
- No primary source for EmberGen-to-Roblox workflows.

## SFX/audio: Audio API vs Sound, upload rules, privacy, licensed library, sourcing, UI sounds, voice

### Takeaway
Roblox now officially discourages Sound, SoundGroup and SoundEffect in favour of the modular Audio API:
- AudioPlayer produces the stream.
- AudioEmitter and AudioListener handle 3D placement.
- AudioDeviceOutput is the speaker.
- Wire connects the pieces.
- Effects include Equalizer, Compressor, Reverb, Fader and Analyzer.

Uploads must be legal, under 20 MB and under 7 minutes. Verified creators get 2,000 free uploads per 30 days; unverified creators get 100. Since March 2022 most user audio is private, so use your own uploads or the Creator Store's 100,000+ licensed tracks and SFX.

### Cited Findings
- "Sound, SoundGroup, and SoundEffect objects are now discouraged in favor of the more robust functionality of audio objects." — [Roblox Docs: Audio objects](https://create.roblox.com/docs/audio/objects)
- Object roles:
  - AudioPlayer loads and plays an asset ID.
  - AudioEmitter is a virtual speaker in 3D.
  - AudioListener is a virtual microphone.
  - AudioDeviceOutput is the real speakers or headphones.
  - AudioDeviceInput is the real microphone, used for voice.
  - AudioTextToSpeech has a 300-character limit per request.
  - AudioSpeechToText converts speech to text.
  - Wire carries a stream from SourceInstance to TargetInstance.

  — [Roblox Docs: Audio objects](https://create.roblox.com/docs/audio/objects)
- 2D audio needs AudioPlayer + AudioDeviceOutput + Wire, placed in SoundService. 3D audio needs AudioPlayer → Wire → AudioEmitter (whose parent sets the position), then AudioListener → Wire → AudioDeviceOutput. The default listener is created on CurrentCamera in voice-enabled experiences. — [Roblox Docs: Audio objects](https://create.roblox.com/docs/audio/objects)
- Effect types: Equalizer, Compressor, Reverb, Chorus, Distortion, Echo, Flanger, Pitch Shift, Tremolo, Fader, Analyzer. — [Roblox Docs: Audio effects](https://create.roblox.com/docs/audio/effects)
- Import requirements:
  - Legal rights to the audio, and compliance with the Community Rules and ToS.
  - A single track in .mp3, .ogg, .wav or .flac.
  - **Under 20 MB and under 7 minutes**.
  - Sample rate of 48 kHz or less.
  - Mono, stereo, 3.0 or 5.1.
  - **2,000 free imports per 30 days if ID-verified, 100 if unverified**. Daily limits have been replaced by this monthly limit.

  Uploads go through a moderation queue. You can import via the Asset Manager, the Creator Dashboard or the Open Cloud Assets API. — [Roblox Docs: Audio assets](https://create.roblox.com/docs/audio/assets)
- The Creator Store has "more than 100,000 professionally-produced sound effects and music tracks from top audio and music partners". Clicking one inserts a legacy Sound; copying the Asset ID lets you use it in an AudioPlayer instead. — [Roblox Docs: Audio assets](https://create.roblox.com/docs/audio/assets)
- Uploads are auto-classified as a sound effect or a song. A song can appear on the game's details page if it passes moderation and copyright checks and the uploader is ID-verified and has accepted the Audio Terms of Use. — [Roblox Docs: Audio assets](https://create.roblox.com/docs/audio/assets)
- March 2022 privacy change:
  - All new audio became private by default, and existing audio **longer than 6 seconds** was made private. Metadata stays visible.
  - The licensed catalog stayed public. It gained 100,000+ rights-cleared songs plus 100,000+ SFX from partners including **APM and Monstercat**.

  Usage permissions can now be granted to specific friends and experiences. — [DevForum: Upcoming Changes to Asset Privacy for Audio](https://devforum.roblox.com/t/1701697); [Roblox Docs: Audio assets](https://create.roblox.com/docs/audio/assets)
- Roblox staff said in Sept 2022 that clips under 6 seconds behaving differently was intended. — [DevForum: 1-second SFX can't be made public](https://devforum.roblox.com/t/1-second-long-sfx-cant-be-made-public/1991394)
- Roblox documents a REAPER workflow for creating audio. — [Roblox Docs: REAPER](https://create.roblox.com/docs/art/reaper)
- Accessibility guidance includes "sound non-reliance" and in-game volume controls (sections exist on the page). — [Roblox Docs: Accessibility](https://create.roblox.com/docs/production/publishing/accessibility)

### Inferences
- Simple mixing setup for a small team: make one AudioFader per bus (Music, SFX, UI), wire every AudioPlayer through its bus fader into one AudioDeviceOutput, and drive the faders from a settings menu. This replaces SoundGroups.
- Keep legacy Sound for quick one-shots only if the team finds wiring too heavy. It still works but is discouraged.
- UI sounds should be short and quiet, varied slightly with Pitch Shift or random pitch, and paired with a HapticEffect of type UIClick on mobile.
- Sourcing: use Creator Store licensed SFX first, then royalty-free libraries whose license allows redistribution inside games (check each license), or record your own. Uploading copyrighted music risks moderation.
- Voice chat: the Audio API routes voice through AudioDeviceInput, so the same effects and emitters can process voice. Design for proximity and moderation.

### Gaps
- Exact voice-chat eligibility rules for 2026 (age/ID requirements, opt-in) were not researched here; I found no source in this pass.
- Did not confirm any official Roblox list of recommended external royalty-free SFX sites.

## Game feel / juice that boosts retention

### Takeaway
Roblox's own design docs make feedback on every action a core UX principle, and recommend celebratory "moments of joy" to end onboarding. Community and general game-feel sources add the techniques: tweened buttons (shrink or grow on click, hover glow), particles, small camera shake, hit-stop and sound. I found no Roblox-published causal data tying specific juice techniques to retention numbers.

### Cited Findings
- Feedback examples given by Roblox:
  - A hit-reaction animation.
  - Buttons that change colour on hover, press and release.
  - A "cha-ching!" sound on purchase.
  - A filling progress bar.

  Missing feedback leaves players unsure whether a feature worked or whether it's broken. — [Roblox Docs: UI and UX design](https://create.roblox.com/docs/production/game-design/ui-ux-design)
- Movement draws attention: "Particle effects, wiggling buttons, and animated arrows are often used in tutorials", but use them in moderation. — [Roblox Docs: UI and UX design](https://create.roblox.com/docs/production/game-design/ui-ux-design)
- "Joy can be elicited through rewards, delightful animations, and celebratory visual effects when a player achieves a milestone." End onboarding on such a moment. — [Roblox Docs: Onboarding](https://create.roblox.com/docs/production/game-design/onboarding)
- The open-source "Visual Tweens" module (MIT) offers Shrink on Click, Grow on Click, Click Glow and Hover effects for Frames and ImageLabels. — [DevForum: Visual Tweens](https://devforum.roblox.com/t/visual-tweens-effect-for-ui/3295455)
- Core juice tools: screen shake (kept small), hit-stop of about 50–100 ms, particles, tweening and easing. — [Wayline: Game feel lesson](https://www.wayline.io/learn/game-feel/1)
- Respect Reduce Motion: when `GuiService.ReducedMotionEnabled` is true, set the TweenInfo time to 0 or fall back to fades. — [Roblox Docs: Accessibility](https://create.roblox.com/docs/production/publishing/accessibility)
- Haptic feedback (UIClick, GameplayCollision) is available on mobile and gamepads. — [Roblox Docs: Mobile input](https://create.roblox.com/docs/input/mobile)

### Inferences
- A juice checklist per action:
  - A visual state change (tween scale 0.95 → 1.05 → 1).
  - A sound.
  - Optionally a haptic.
  - For rewards: particle burst, number pop-up and counter tick-up.

  Validate the impact with Experiments (A/B tests) rather than assuming it.

### Gaps
- No Roblox-specific quantitative study linking juice to D1 or D7 retention.
- No official Roblox camera-shake API or tutorial was found.

## Accessibility and localization

### Takeaway
Roblox exposes player accessibility preferences that UI should respect: PreferredTextSize, PreferredTransparency and ReducedMotionEnabled. It also recommends contrast, no reliance on colour alone, and no reliance on sound alone. Automatic translation (Automatic Text Capture plus auto-translate, within quotas) localizes UI strings for free, controlled per object by AutoLocalize.

### Cited Findings
- **Text Size** maps to `GuiService.PreferredTextSize` (Medium by default, up to Large, Larger or Largest). A UITextSizeConstraint caps text even when the player enlarges it, so avoid tight max sizes. — [Roblox Docs: Accessibility](https://create.roblox.com/docs/production/publishing/accessibility)
- **Background Transparency** maps to `GuiService.PreferredTransparency`. The recommended pattern multiplies an element's BackgroundTransparency by it and listens for changes. — [Roblox Docs: Accessibility](https://create.roblox.com/docs/production/publishing/accessibility)
- **Reduce Motion** maps to `GuiService.ReducedMotionEnabled`. Snap tweens (time 0) or use fades instead. — [Roblox Docs: Accessibility](https://create.roblox.com/docs/production/publishing/accessibility)
- Colour: "Over 5% of people in the world have some form of color blindness". Pair colours with symbols, and check the UI in grayscale. Make sure there is enough text and background contrast. — [Roblox Docs: Accessibility](https://create.roblox.com/docs/production/publishing/accessibility)
- Cross-platform checklist: text legible on all screens, sufficient contrast, nothing relying solely on colour. — [Roblox Docs: Cross-platform development](https://create.roblox.com/docs/projects/cross-platform)
- Automatic Text Capture (ATC) collects UI strings that players or Studio testing encounter, and only from objects with `AutoLocalize` enabled. Disable AutoLocalize on names and signs. ATC automatically removes stale strings. Auto-translation fills only blank entries and never overrides manual translations. Languages are toggled per language in the localization settings. There are initial and monthly translation quotas. — [Roblox Docs: Automatic translation](https://create.roblox.com/docs/production/localization/automatic-translations); [Roblox Docs: Localization](https://create.roblox.com/docs/production/localization)
- Dynamic content (scripted strings) has separate docs on auto-translating dynamic content and on localizing with scripting. — [Roblox Docs: Auto-translate dynamic content](https://create.roblox.com/docs/production/localization/auto-translate-dynamic-content)
- AudioTextToSpeech and AudioSpeechToText exist as audio objects. They could support assistive narration or captions. — [Roblox Docs: Audio objects](https://create.roblox.com/docs/audio/objects)

### Inferences
- Design layouts with roughly 30–40% extra text room for translated strings (German or Portuguese, for example) by using AutomaticSize and flex layouts. Prefer TextScaled with generous UITextSizeConstraint limits.
- Subtitles and captions: there is no built-in subtitle system for game audio. Implement captions as a TextLabel that displays alongside key sounds, in line with "sound non-reliance".

### Gaps
- No official Roblox colourblind filter or mode was found. Designers must handle it through palettes and symbols.
- Exact automatic-translation quota numbers were not extracted, and no built-in subtitle feature was confirmed.
