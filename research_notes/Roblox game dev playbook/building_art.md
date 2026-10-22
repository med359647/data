# Roblox Building / 3D Art / World-Creation Pipeline (as of Oct 2026)

> Research method note: create.roblox.com and devforum.roblox.com did not resolve from the research environment (DNS failure). Official doc content was read from Roblox's public docs source repo (github.com/Roblox/creator-docs, `main` branch, fetched 2026-10-22), which is what create.roblox.com is built from. DevForum content comes from search-result snippets only, not full-page reads, so treat DevForum-derived points as lower confidence. Third-party sites are labeled.

## Tools: Studio building, Blender pipeline, meshes/textures, generative AI

### Takeaway
The standard 2026 pipeline is: block out in Studio (parts, terrain), then model hero and repeated assets in Blender. Export each repeated mesh once (FBX/glTF/OBJ at 0.01 scale) and import it with the 3D Importer as a MeshPart, with SurfaceAppearance PBR on top. Hard limits are 20,000 triangles per mesh and textures up to 4096x4096 (4K rendering is now supported). Practical budgets are far lower: 512px or less for most textures. Roblox's AI tools (Cube 3D mesh generation, Texture Generator, Avatar/Accessory Auto-Setup, 4D generation) exist but are mostly beta or "in active development". Use them for prototyping and filler, not for the hero art pipeline.

### Cited Findings
**Mesh specs (official)**
- "Individual meshes can not exceed 20,000 triangles." Avatar items have separate budgets. Geometry should be watertight, with no exposed holes or backfaces and real thickness (not zero-thickness). Use quads where possible and avoid N-gons — [creator-docs: art/modeling/specifications](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/art/modeling/specifications.md)
- Rigging: freeze bones at scale 1,1,1 and rotation 0,0,0. The root bone goes at 0,0,0 with no influences on it, and each vertex can have at most 4 bone influences. Only one animation track exports per mesh or model, so each animation is exported separately (.fbx) — [same](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/art/modeling/specifications.md)
- Layered-clothing cages use the `_InnerCage` / `_OuterCage` suffixes. Characters need an outer cage to equip layered accessories — [same](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/art/modeling/specifications.md)
- Third-party and older figures conflict. Some cite a ~21k ceiling, ~10k for batch import, or the old 10k mesh limit (DevForum 2022 thread, now OUTDATED). Use the official 20k figure — [Nilo blog (vendor)](https://nilo.io/articles/vibe-code-roblox-triangle-limit); [DevForum: Exceed 10,000 triangle limit (old)](https://devforum.roblox.com/t/exceed-10000-triangle-limit/1760555)

**Textures / PBR (official)**
- "Roblox supports up to 4096×4096 pixel texture resolutions (4K)." The same page still says "up to 1024×1024 pixel spaces for texture maps" in its UV section, and 1024x1024 is the maximum PBR budget for full-body clothing and humanoid characters. The doc is internally inconsistent, which suggests the 1024 references are leftovers from before 4K — [creator-docs: texture-specifications](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/art/modeling/texture-specifications.md)
- 4K texture rendering was announced at RDC 2025 ("later this year"). A DevForum "4K Texture Rendering" announcement exists (t/4316229, early 2026 by thread number) — [allthings.how RDC recap (3rd party)](https://allthings.how/roblox-rdc-2025-10-creator-tools-and-updates-that-matter/); [DevForum 4K texture rendering](https://devforum.roblox.com/t/4k-texture-rendering/4316229); [MoguraVR (JP) on Cube 4D + 4K textures GA](https://www.moguravr.com/roblox-cube-foundation-model-4d-generation-4k-texture/)
- PBR maps: Albedo RGB 24-bit; Normal RGB (OpenGL, tangent space only); Roughness, Metalness and Emissive Mask as 8-bit grayscale. Emissive maps were announced at RDC 2025 for end of year and now appear in the official spec — [texture-specifications](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/art/modeling/texture-specifications.md); [allthings.how](https://allthings.how/roblox-rdc-2025-10-creator-tools-and-updates-that-matter/)
- Size guidance by object size: 1-stud cube 64–128px; 2-stud 256px; 4-stud 512px; 8-stud 1024px. Textures are uploaded as .png/.jpg/.tga/.bmp. Each mesh has one UV set, with all UVs in 0–1 (overlaps allowed) and one material per mesh object. SurfaceAppearance overrides MeshPart.TextureID — [same](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/art/modeling/texture-specifications.md)

**Blender → Studio**
- OBJ/glTF export: Transform scale 0.01, Forward Z, Up Y, "Limit to Selected Objects". FBX: Unit Scale 0.01 or export scale 0.01, with Apply Scalings set to "FBX Unit Scale". In Studio's Import Preview, set Scale Unit = Stud. Newer docs show an "Import Only as a Model" option, and the menu path differs by version ("File > Import 3D") — [create.roblox.com/docs/art/blender (via search snippets)](https://create.roblox.com/docs/art/blender)
- RDC 2025 roadmap: one-click model re-import and Animation Reimport. These are important for iterating on Blender assets without breaking references. Shipping status was not verified — [allthings.how](https://allthings.how/roblox-rdc-2025-10-creator-tools-and-updates-that-matter/)

**Generative AI tools (status)**
- Cube 3D launched March 2025 (beta) as text-to-mesh in Studio and via an in-experience Lua API, with an open-source model. In February 2026 Roblox launched "4D generation" on the Cube Foundation Model: players generate functional objects using the schemas "Car-5" (modular vehicles with working wheels) and "Body-1" (single mesh). Image-to-3D and custom schemas are in research. Wish Master reportedly saw 160K+ items generated, and a creator claimed +64% playtime (single-creator claim) — [ssojet summary](https://ssojet.com/news/roblox-launches-cube-3d-ai-model-for-3d-and-future-4d-creation); [MoguraVR](https://www.moguravr.com/roblox-cube-foundation-model-4d-generation-4k-texture/); [TechCrunch](https://techcrunch.com/?p=2981320)
- Texture Generator is still a beta (File > Beta Features). Roblox's Creator Updates page describes a "Quality mode" beta that generates 4K PBR textures. For repeating surfaces Roblox points to Material Generator instead — [promptblox (3rd party)](https://promptblox.ai/roblox-ai); [create.roblox.com/updates (snippet)](https://create.roblox.com/updates)
- Avatar Auto-Setup reached production in late 2024 and is "still in active development". A May 2026 update added eyebrows, eyelashes, decal faces and higher-fidelity rigs. Accessory Auto-Setup entered beta in March 2026 and outputs EditableMesh/EditableImage; there is also an in-experience Accessory Auto-Setup client beta — [DevForum: Avatar Auto-Setup update](https://devforum.roblox.com/t/avatar-auto-setup-update-new-support-for-eyebrows-decal-faces-and-higher-fidelity-rigs/4634673); [DevForum: in-experience accessory auto-setup beta](https://devforum.roblox.com/t/client-beta-in-experience-accessory-auto-setup/4358192); [promptblox](https://promptblox.ai/roblox-ai)
- A "Prompt to Avatar" tool was reportedly announced at RDC 2026 (September) for end of 2026. This is third-party only and unverified — [promptblox](https://promptblox.ai/roblox-ai)
- RDC 2025 also announced in-experience CSG on meshes and a cloud transcoding pipeline / "Harmony" that optimizes assets per device tier — [allthings.how](https://allthings.how/roblox-rdc-2025-10-creator-tools-and-updates-that-matter/)

### Inferences
- With 4K now possible, the real constraint is memory, not the cap: stick to the 512px default from the performance docs (see Performance) and reserve 1024+ for a few hero assets.
- Treat the 20k-triangle cap as a ceiling. Aim for roughly 500–5k triangles for props repeated many times, because instancing and memory matter more than the cap. This is a heuristic, not an official number.
- AI mesh output should go through a cleanup step (triangle count, collision set to Box/Hull, consistent texel density) before entering the kit.

### Gaps
- Could not verify current details for the CSG/Solid Modeling engine, the terrain editor 2026 changes, or the status of the F3X / Building Tools by F3X / Archimesh plugins. Note that Archimesh is a Blender add-on for architecture, not a Studio plugin, and F3X is a long-standing free Studio building plugin; these points come from the researcher's background knowledge and were not freshly sourced.
- The official "Roblox Blender plugin" (Studio-Blender sync add-on) was not confirmed in sources.
- Could not confirm whether Material Generator changed in 2025–26, or the current daily limits for the AI tools.

## Lighting

### Takeaway
OUTDATED: the Future/ShadowMap/Voxel choice. "Unified Lighting" went fully live July 23, 2025 and replaced `Lighting.Technology` with `LightingStyle` (Realistic / Soft) and `PrioritizeLightingQuality` (bool). The engine now scales lighting quality per device automatically. Small teams should pick a style and a priority flag, then cut light count, shadow casters and transparency for mobile.

### Cited Findings
- `Lighting.Technology` "has been superseded by LightingStyle and PrioritizeLightingQuality". The Legacy, Compatibility and Unified values are deprecated and cannot be selected in Studio. Voxel is a 4×4×4 voxel map; ShadowMap gives crisp sun shadows; Future is "the most advanced" — [creator-docs: Technology enum](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/reference/engine/enums/Technology.yaml)
- Migration mapping: Future becomes Realistic + PrioritizeLightingQuality on; ShadowMap becomes Soft + on; Voxel becomes Soft + off. Unified Lighting was a Studio beta from January 2025 and fully live July 23, 2025 — [DevForum: Unified Lighting is Fully Live (snippet)](https://devforum.roblox.com/t/let-there-be-unified-light-unified-lighting-is-fully-live/3401512); [Bloxy News](https://x.com/Bloxy_News/status/1881791225822327102)
- PrioritizeLightingQuality decides whether lighting quality or view distance is reduced first when rendering quality drops. ShadowSoftness applies only to Realistic. Other Lighting properties: Ambient/OutdoorAmbient, Brightness, ExposureCompensation, GlobalShadows, EnvironmentDiffuseScale/SpecularScale, ClockTime, GeographicLatitude — [creator-docs: environment/lighting](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/environment/lighting.md)
- Roblox suggests Voxel + ColorGradingEffect with the "Retro" tonemapper to recreate the old Compatibility look. This confirms a ColorGradingEffect post-process exists — [Technology enum](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/reference/engine/enums/Technology.yaml)
- Early reports said Realistic reverted to Soft in published games. That was a beta-era bug and its fix status was not verified — [DevForum thread (snippet)](https://devforum.roblox.com/t/lightingstyle-property-keeps-changing-to-soft-only-in-game/3437295)
- Performance doc guidance: shadows are disabled automatically below graphics quality level 4. Disable CastShadow on small or distant parts and moving objects, turn off Light.Shadows where not needed, limit light Range/Angle, and use fewer lights. Avoid overlapping semi-transparent objects (overdraw) — [creator-docs: performance-optimization/improve](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/performance-optimization/improve.md)
- The Unified Lighting announcement said it lays the foundation for increased light ranges and light attenuation — [Bloxy News](https://x.com/Bloxy_News/status/1881791225822327102)

### Inferences
- For mobile-heavy audiences: use LightingStyle = Soft with PrioritizeLightingQuality off unless lighting is core to the mood (horror), and bake the mood with Atmosphere, ColorCorrection/ColorGrading, and a Sky rather than many dynamic lights.

### Gaps
- No fresh primary source on Atmosphere/Bloom/DepthOfField/SunRays costs on mobile, or on any 2026 lighting features beyond Unified Lighting and emissive maps.

## Performance

### Takeaway
The biggest wins come from: (1) instance streaming with aggressive radii and few Persistent models; (2) reusing a single uploaded mesh and texture so copies instance into one draw call; (3) small textures (512px or less, 256px for minor items); (4) Box collision with CanCollide/CanTouch/CanQuery off on decorative parts, and anchoring everything static; (5) SLIM level-of-detail (the replacement for old model LOD); (6) limiting shadows, lights and transparency.

### Cited Findings
- Draw calls: fewer per frame means faster rendering. Check them in Render Stats (Shift+F2). Meshes with the same MeshContent instance into one draw call only if their SurfaceAppearance or TextureContent also match. Reimporting a whole map can give identical meshes different IDs and break instancing, so upload each mesh once and duplicate it in Studio — [improve.md](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/performance-optimization/improve.md)
- Decals, textures and particles batch poorly. Set RenderFidelity to Automatic or Performance and avoid Precise on many meshes — [same](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/performance-optimization/improve.md)
- LOD: enable instance streaming, set `Model.LevelOfDetail = SLIM`, and set `Workspace.EnableSLIMAvatars`. SLIM ("Scalable Lightweight Interactive Models") was announced at RDC 2025 to replace the older Model LOD (StreamingMesh) — [improve.md](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/performance-optimization/improve.md); [allthings.how](https://allthings.how/roblox-rdc-2025-10-creator-tools-and-updates-that-matter/)
- Physics: anchor parts that don't need physics. Collision fidelity should be Box for small or non-interactive items, Box or Hull for medium items, and custom invisible parts for large complex objects. Box has the lowest memory, while Default and Precise cost more. Set CanCollide/CanTouch/CanQuery = false for parts that need no collision, and use Box or Hull even then because collision geometry stays in memory. Adaptive physics stepping runs at 60/120/240 Hz, while Fixed is 240 Hz and costly — [same](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/performance-optimization/improve.md)
- Textures: memory depends on pixel count; a 1024² texture uses 4x the memory of a 512². Compression and stripping alpha don't help because Roblox transcodes images. Images rarely need more than 512²; minor ones should be under 256². Tint a single texture with SurfaceAppearance.Color, and use trim sheets — [same](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/performance-optimization/improve.md)
- Skinned MeshParts without a Humanoid rebuild spatial clusters when they move — [same](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/performance-optimization/improve.md)
- Streaming is "the highest-impact" memory and load-time improvement and is on by default for new places. Defaults: StreamingMinRadius 64, StreamingTargetRadius 1024, StreamOutBehavior LowMemory (Opportunistic recommended). ModelStreamingBehavior Improved is recommended over Legacy, and StreamingIntegrityMode PauseOutsideLoadedArea is recommended. PredictiveStreamingMode is opt-in and skipped on low-resource devices. Streaming modes: Nonatomic (default), Atomic, Persistent (never streams out; "overuse may negatively impact performance"), and PersistentPerPlayer — [creator-docs: workspace/streaming](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/workspace/streaming/index.md); [improve.md](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/performance-optimization/improve.md)
- Nesting a Persistent model inside an Atomic one forces the parent to behave as Persistent. Large "container" models reduce streaming efficiency and are bad for model LOD, which works best on closely grouped instances — [create.roblox.com streaming techniques (snippet)](https://create.roblox.com/docs/workspace/streaming/techniques)
- Instance Streaming inside Studio (editing huge worlds without loading everything) was on the RDC 2025 roadmap — [allthings.how](https://allthings.how/roblox-rdc-2025-10-creator-tools-and-updates-that-matter/)
- A common streaming pitfall: client scripts that assume Workspace instances exist on join (use WaitForChild) — [improve.md](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/performance-optimization/improve.md); [gamertagmythras guide (3rd party)](https://gamertagmythras.com/blog/roblox/roblox-instance-streaming-guide)

### Inferences
- Organize maps as many small, spatially compact Models (one building = one Model) rather than giant folders. Mark interactables Atomic, and avoid Persistent except for a few core items such as the lobby spawn.
- Keep a "decor" convention: Anchored = true, CanCollide/CanTouch/CanQuery = false, CollisionFidelity = Box, CastShadow = false for small items. A small command-bar script or plugin can enforce it.

### Gaps
- No official numeric budgets were found for part count, draw calls or memory on low-end phones. Roblox's docs avoid hard numbers. Community rules of thumb (for example, keeping draw calls in the low hundreds on mobile) could not be sourced in this pass.
- The official status of Packages (auto-update, versioning) in 2026 was not refreshed.

## Asset sourcing, Creator Store, reuse

### Takeaway
The Creator Store now lets sellers sell Models and Plugins for USD (they keep 100% of net). Free models remain a malware risk; Roblox bans obfuscation, `require`/`loadstring`-style remote loading and the like, but teams should still Disable Scripts on insert and audit. Asset Privacy (Restricted by default) governs who can load meshes and images, so group ownership matters.

### Cited Findings
- Store categories are 3D, VFX, 2D, Gameplay, Plugins and Audio. Only Models and Plugins can be sold, in USD via a Stripe seller account. Prices run $2.99–$49.99 for models and $4.99–$249.99 for plugins; sellers keep 100% of net proceeds; there is a 30-day escrow with monthly payouts. Only individually owned assets can be sold, not group assets — [creator-docs: production/creator-store](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/production/creator-store.md)
- Prohibited: obscuring engine features (getfenv/setfenv, Lua VMs), remote loading (`loadstring()`, `InsertService:LoadAsset()`, LinkedSource), obfuscation, and unnecessarily large scripts. To check an asset, right-click it in Explorer, choose Disable Scripts, and inspect. Report violations via Report Item — [same](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/production/creator-store.md)
- Monthly distribution caps: verified accounts get 200 meshes/images/models, 100 audio, 10 plugins; unverified get 10 each and 2 plugins — [same](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/production/creator-store.md)
- Asset Privacy: Restricted vs Open Use. A restricted asset "cannot load in Studio or at runtime" without the owner's permission; it is "not DRM". Group sharing requires "Edit all group experiences" permission, and the asset is usable only in group-owned experiences — [creator-store.md](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/production/creator-store.md); [create.roblox.com asset privacy (snippet)](https://create.roblox.com/docs/projects/assets/privacy)

### Inferences
- Have the group own all uploads (meshes, images, animations) from day one, to avoid permission breakage when a member leaves.
- Build a modular kit (walls, floors, trims on a fixed grid, for example 4 or 8 studs) with shared trim-sheet textures. Publish it as Packages so edits propagate. This aligns with the instancing guidance to upload each mesh once.

### Gaps
- 2026 Packages features (auto-update, version history UI) and creator-store licensing beyond these terms were not verified.

## Characters & animation

### Takeaway
R15 is the default and is required for layered clothing and modern avatar features. R6 remains a stylistic choice for simple, combat-heavy games. Animations are not interchangeable between rigs. Animation ownership is the classic trap: animations must be owned by the experience owner (group) or explicitly shared. Roblox added connection and group sharing in 2025, but docs and forum posts disagree on its scope.

### Cited Findings
- An R15-made animation only works on R15 rigs, and vice versa — [DevForum thread (snippet)](https://devforum.roblox.com/t/animations-suddenly-limiting-change-not-in-changelog/1547537)
- The built-in Animation Editor offers keyframes, easing and IK, and supports R6 and R15. Moon Animator 2 is described as the most popular advanced plugin (curves, multi-track, camera, cutscenes). A BuiltByBit listing updated May 2026 sells it for $14.99 and claims R6, R15 and custom skinned mesh support; this is seller and promotional info — [creation.dev roundup (3rd party)](https://www.creation.dev/tools/animation-plugins); [BuiltByBit listing](https://builtbybit.com/resources/moonanimator-2.109718/)
- 2025: animations moved into asset privacy, with sharing to connections and groups via a Permissions option in Creator Hub plus experience-level grants. Sharing via models/packages was "next" — [DevForum: Sharing Animation Assets with Connections and Groups (snippet)](https://devforum.roblox.com/t/sharing-animation-assets-with-connections-and-groups/3892540). The current asset-privacy doc says Animations' creation defaults are not changed by the Asset Privacy setting — [create.roblox.com asset privacy (snippet)](https://create.roblox.com/docs/en-us/projects/assets/privacy). These are partially conflicting; verify in Creator Hub.
- Avatar Auto-Setup turns a static mesh into a rigged, caged avatar body (May 2026 update: eyebrows, eyelashes, decal faces) — [DevForum](https://devforum.roblox.com/t/avatar-auto-setup-update-new-support-for-eyebrows-decal-faces-and-higher-fidelity-rigs/4634673)
- Animation Graphs appear in the 2025 end-of-year roadmap recap. Animation Reimport and SLIM avatars (EnableSLIMAvatars) were RDC 2025 items — [DevForum end-of-year recap (snippet)](https://devforum.roblox.com/t/creator-roadmap-2025-end-of-year-recap/4156739); [allthings.how](https://allthings.how/roblox-rdc-2025-10-creator-tools-and-updates-that-matter/)

### Gaps
- Animation capture (camera-based body tracking) status for 2026 was not refreshed.
- Rig importing specifics beyond the mesh spec (4 influences, root at origin) were not refreshed.

## Style choices and how top games look

### Takeaway
No fresh primary sources were gathered in this pass. Recommendations below are inference.

### Cited Findings
- Roblox's own guidance favors reusable tinted textures, trim sheets and few unique textures, all of which favor stylized and low-texture art — [improve.md](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/performance-optimization/improve.md)

### Inferences
- Stylized low-poly with flat or gradient trim-sheet palettes (one 512–1024 atlas shared across the kit, tinted via SurfaceAppearance.Color or part Color) instances well, stays light on memory for mobile, and ships fast. Soft lighting style plus ColorGrading gives a cohesive look cheaply.
- Most top 2025–26 front-page titles (simulators, "grow a garden"-style games, obbies, hangout games) lean on bright, simple, readable stylized art rather than realism. This is background knowledge, not freshly sourced.

### Gaps
- No sourced analysis of art direction in top 2025–26 Roblox games, and no creator YouTube or guide citations, were gathered due to the tool-call budget.
