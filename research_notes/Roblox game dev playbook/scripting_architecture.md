# Reusable Roblox (Luau) Scripting Architecture and Toolchain, as of October 2026

Research notes, 22 Oct 2026. Method note: create.roblox.com and devforum.roblox.com could not be fetched directly in this session (DNS/proxy block). Claims from those domains come from search-result excerpts of those pages, not full reads. GitHub pages were fetched directly. Where a claim relies only on prior knowledge and could not be re-verified, it is placed under Inferences or Gaps, not Cited Findings.

## 1. Project structure and frameworks (Knit, Flamework, plain module loaders, ECS/jecs)

### Takeaway
Knit is officially archived (July 2024) and should not be used for new games. Its author says the "services" architecture can be built from plain ModuleScripts. The simplest maintainable foundation for a small, Luau-new team is one server bootstrap Script plus one client bootstrap LocalScript. Each requires a folder of plain ModuleScript "services" (server) or "controllers" (client) and calls their Init then Start functions. Add an ECS (jecs) only for simulation-heavy games. Flamework only makes sense if the team moves to TypeScript (roblox-ts).

### Cited Findings
- Knit's GitHub repo "was archived by the owner on Jul 31, 2024. It is now read-only"; the README says "Knit has been archived and will no longer receive updates." — [Sleitnick/Knit GitHub](https://github.com/Sleitnick/Knit)
- Why Knit was archived, from the author's ARCHIVAL.md: Knit "cannot fully benefit from types, and thus does not have good intellisense." Knit's role #1, a service-like architecture, "is easy to replicate, as ModuleScripts themselves can already work in this way out of the box." Role #2, networking, is "harder" because "any networking tool is going to be a wrapper on top of RemoteEvents, UnreliableRemoteEvents, and RemoteFunctions". Luau types "do not enforce the underlying data", so network data "requires runtime type-checking", e.g. "using `assert` on a variable coming over a RemoteFunction to ensure it's a `number`". — [Knit ARCHIVAL.md](https://raw.githubusercontent.com/Sleitnick/Knit/main/ARCHIVAL.md)
- Community Knit successors still appear, e.g. "OwlKnit", which its author presents as a maintained, MIT-licensed spiritual successor. This is self-promotion, and I found no independent endorsement. — [DevForum: OwlKnit](https://devforum.roblox.com/t/owlknit-a-modern-and-knit-inspired-framework-v112/4761632)
- Flamework is "a TypeScript game framework designed for simplicity". It offers constructor dependency injection and "automatically generates type guards for your networking code and components". It belongs to the roblox-ts ecosystem, not plain Luau. — [Flamework docs](https://flamework.fireboltofdeath.dev/docs/introduction)
- jecs is described as a "high-performance ECS library for Roblox (Luau)" with archetypes, type safety and "first-class entity relationships"; community templates exist. — [LocalPulse/jecs-template](https://github.com/LocalPulse/jecs-template)
- ECS on Roblox is argued for as composition over inheritance. "Components" are data-only tables such as health or speed, and "systems" hold the logic. — [DevForum: ECS in Roblox Studio](https://devforum.roblox.com/t/ecs-in-roblox-studio-why-is-it-better-than-oop-and-how-to-cook-it/3962745)
- Sleitnick's RbxUtil, a maintained utility suite, covers networking (Net, Comm, TypedRemote), data (BufferUtil, Ser, TableUtil), physics (PID, Spring, Quaternion) and lifecycle cleanup (Trove). It is published through Wally and npm. — [RbxUtil docs index](https://docsearch.algolia.com/mcp/docs/repo/sleitnick/rbxutil)

### Inferences
- Recommended folder layout. This is standard Roblox replication behaviour, and it matches the Rojo default project template:
  - `ServerScriptService/Server/Main.server.luau`: the single server entry point. `ServerScriptService/Server/Services/*.luau` holds the services (DataService, PurchaseService, CombatService…). Neither is visible to clients, so secrets and authoritative logic live here.
  - `ServerStorage/`: server-only assets, such as maps to clone and admin tools.
  - `ReplicatedStorage/Shared/`: modules both sides require, such as config tables, type definitions and pure utility functions. `ReplicatedStorage/Packages/` holds Wally/pesde dependencies. `ReplicatedStorage/Remotes` or a generated network module holds the networking layer.
  - `StarterPlayer/StarterPlayerScripts/Client/Main.client.luau`: the single client entry point. `.../Controllers/*.luau` holds the controllers (UIController, InputController, SoundController).
  - Why it matters: everything in ReplicatedStorage and on the client can be read, and modified, by exploiters. Keeping logic split by trust boundary is the first security measure.
- Module-loader pattern: Main requires every ModuleScript in Services, calls `:Init()` on all of them (wiring only, no yielding), then `task.spawn`s `:Start()` on each. This replaces Knit in about 30 lines. It keeps load order predictable and gives full Luau type inference, because each service is a plain `require`.
- Framework recommendation for a small team: plain modules plus a loader, a typed network layer, ProfileStore, and Trove/Signal. Add jecs only if the game has many similar entities (NPC swarms, projectiles, tower defense). An ECS adds a conceptual hurdle for beginners.

### Gaps
- I found no authoritative 2026 survey of which architecture "experienced devs" prefer. The DevForum discussions surfaced were opinion threads. The "plain modules" consensus rests mainly on the Knit author's archival note.
- "Lune" (a standalone Luau runtime used for build scripts and tooling) was not researched in depth in this session. pesde lists Lune as a target (see section 2).

## 2. Tooling: Rojo, package managers, linting, types, editors, Git, Script Sync, Studio MCP, AI assistance

### Takeaway
There are two viable workflows in 2026:
- **Studio-first:** Team Create plus Roblox's built-in Script Sync to edit scripts in VS Code and keep them in Git.
- **Filesystem-first:** Rokit (toolchain manager), Rojo, Wally or pesde, Selene, StyLua and luau-lsp in VS Code, with Git as the source of truth.

Roblox now ships an official Studio MCP server, so AI coding agents can read the DataModel, write scripts, run Luau and start playtests. The Studio Assistant can also use external LLMs with your own API key.

### Cited Findings
- Studio Script Sync is built in. It links Studio scripts to files on local disk so they can be edited in an external editor and version-controlled. Roblox's docs say third-party tools like Rojo are a better choice for whole-project version control, or for making the file system the source of truth. — [Creator Docs: Script Sync](https://create.roblox.com/docs/scripting/sync) (search excerpt)
- Rojo lets developers "work from the filesystem, in your favorite editor and version their game using Git or another VCS". — [rojo-rbx/rojo](https://www.github.com/rojo-rbx/rojo)
- Rokit is a toolchain manager, not a package manager, and it "is meant to replace Foreman and Aftman" for installing tools like Rojo. — [rojo-rbx/rokit](https://github.com/rojo-rbx/rokit)
- pesde is a Luau package manager targeting Roblox and Lune. It has its own registry but can also pull Wally and Git packages; the latest crate seen was 0.7.3. — [docs.rs pesde](https://docs.rs/crate/pesde/latest)
- Wally remains widely used. A competitor (Forest) claims Wally's link modules break type resolution unless you run a tool like `wally-package-types` after each install. Treat this as one side's claim. — [DevForum: Forest Package Manager](https://devforum.roblox.com/t/forest-package-manager-the-modern-package-platform-for-roblox/4766024)
- Wally packages land in a `Packages/` folder, which must be mapped into the DataModel (usually ReplicatedStorage) through the Rojo project file. — [roblox-game-skill tooling reference](https://mintlify.wiki/brockmartin/roblox-game-skill/reference/tooling-ecosystem)
- Luau's New Type Solver has exited beta. A Roblox podcast summary cites a DevForum post "General release: Luau's new type solver", and later release notes continue solver fixes, e.g. "greatly improves the ability to infer types of table literals". The exact GA date is unverified (likely late 2025). — [Beyond the Blox podcast summary](https://music.amazon.co.uk/podcasts/b8dc7855-a255-462e-a0fe-aa83cd594319/episodes/02db1176-c7bd-4e1c-8fc6-b6df2fdf9fa5/beyond-the-blox-a-feast-of-roblox-dev-features-for-thanksgiving); [Release notes 664](https://create.roblox.com/docs/release-notes/release-notes-664); [Release notes 675](https://create.roblox.com/docs/release-notes/release-notes-675)
- Roblox ships an official Studio MCP server, "an implementation of the Model Context Protocol" that lets an AI client explore the data model, write scripts, execute Luau and do play-mode testing. It requires the latest Studio and a local MCP client. — [Creator Docs: Studio MCP](https://create.roblox.com/docs/studio/mcp) (search excerpt)
- A February 2026 update added MCP tools to read playtest console output, start and stop play mode, run scripts in play mode, and get the current Studio mode. The Studio Assistant gained bring-your-own-API-key support for external LLMs, Claude included. — [MoguraVR (Japanese)](https://www.moguravr.com/roblox-studio-mcp-server-agentic-update/)
- Third-party MCP servers also exist, such as boshyxd/robloxstudio-mcp, a community plugin plus server. Prefer the official one. — [mcpservers.org listing](https://mcpservers.org/ko/servers/boshyxd/robloxstudio-mcp)
- RbxSync is a newer third-party sync tool (CLI, Studio plugin, VS Code extension) that syncs Studio with the filesystem for Git. A comparison page claims it supports MCP where Rojo, Argon and Pesto do not; that claim is unverified. — [RbxSync docs](https://docs.rbxsync.dev/getting-started/); [glama.ai](https://glama.ai/mcp/servers/gaaj6hnob4)

### Inferences
- For a team with limited Luau experience, start Studio-first: Team Create plus Script Sync plus Git for scripts. Move to Rojo once someone is comfortable with the command line. Rojo pays off when you want one template repo reused across many games: `git clone` the template, `rokit install`, `wally install`, `rojo serve`.
- Put `--!strict` at the top of every new module. The new solver produces fewer false positives than the old one, so strict mode is now practical for beginners, and its errors catch nil and typo bugs before playtest.
- Selene (linter) and StyLua (formatter) are the long-standing defaults in the Rojo ecosystem, installed via Rokit and run in CI. Neither was re-verified this session.
- AI workflow: Claude Code or another agent, plus the official Studio MCP, plus Rojo/Script Sync files on disk. The agent can edit files, start a playtest and read the console. Keep AI-written code behind the same review and lint/type gates as human code. Never let an agent hold publish credentials for the production place.

### Gaps
- I found no evidence of native Git integration inside Studio as of October 2026. Built-in version history (snapshots on publish/save) is the only first-party versioning seen. Search results were low-quality SEO pages.
- Current Selene/StyLua/luau-lsp versions and any 2026 changes were not verified.
- Whether Script Sync supports non-script instances (models, UI) was not confirmed. The docs excerpt implies scripts only.

## 3. Data: DataStore limits, ProfileStore, OrderedDataStore, MemoryStore, migrations, BindToClose

### Takeaway
Use ProfileStore (the successor to ProfileService, which is no longer supported) for all per-player data. It gives session locking, so data can't load on two servers and be duplicated or rolled back, and it handles periodic auto-save. Use OrderedDataStore for leaderboards and MemoryStoreService for cross-server ephemeral state. Store a `Version` number in each profile and run migration functions on load.

### Cited Findings
- ProfileStore "loads and caches data from a DataStore key on one game server and blocks other servers from accessing that data too early by establishing a session lock". It tracks the owning server and hands off ownership "without failing new session requests". It is built for per-player data and is "not designed (and never will be) for in-game leaderboards or any kind of global state." Apache-2.0, by loleris. Docs: https://madstudioroblox.github.io/ProfileStore/ — [MadStudioRoblox/ProfileStore](https://github.com/MadStudioRoblox/ProfileStore)
- ProfileService is no longer supported; ProfileStore is recommended for new projects. Session locking prevents duplication exploits, e.g. in trading games where a second server loads stale data before the first saves, and prevents "data regression". — [DevForum: ProfileStore](https://devforum.roblox.com/t/profilestore-save-your-player-data-easy-datastore-module/3190543/)
- A forum post says ProfileStore will "steal" a dead session's lock after a built-in timeout of about 80 seconds. This is community-reported. — [ProfileStore README mirror / DevForum discussion](https://github.com/ISFOR1/ProfileStore)
- Official limits: 4,194,304 characters (4 MB) per key, and a 50-character maximum for data store name, key and scope. Per-key throughput is checked over the last 60 seconds across all servers, and throttling surfaces as `DatastoreThrottled` or `KeyThrottled`. — [Creator Docs: Data store error codes and limits](https://create.roblox.com/docs/cloud-services/data-stores/error-codes-and-limits.md)
- The often-quoted write budget of "60 + #players × 10" per minute comes from a community post and was not verified against current docs. — [DevForum: DataStore limits](https://devforum.roblox.com/t/game-resourcesdatastore-limits/856634)
- Roblox announced "Unifying Data Stores Open Cloud and Game APIs, and Increasing Storage Limits". The discussion references the 4 MB key cap and a storage allowance per player of around 1 MB (lifetime-user-based). The Data Stores Manager computes the storage limit from lifetime users and shows estimated monthly cost for overages. — [DevForum announcement thread](https://devforum.roblox.com/t/unifying-data-stores-open-cloud-and-game-apis-and-increasing-storage-limits/4739240?page=3); [Creator Docs: Data Stores Manager](https://create.roblox.com/docs/en-us/cloud-services/data-stores/data-stores-manager)
- Open Cloud data store rate limits are per universe, are the same for v1 and v2, and return HTTP 429 when exceeded. — [Creator Docs: Throttling](https://create.roblox.com/docs/en-us/cloud/guides/data-stores/throttling.md)

### Inferences
- Template pattern:
  - DataService wraps ProfileStore. It loads a profile on PlayerAdded, calls `Reconcile` to fill new default fields, and runs the `migrations[profile.Data.Version]` chain. It kicks the player if the load fails, and releases the profile on PlayerRemoving.
  - Never call SetAsync per stat change. Mutate `Profile.Data` in memory and let ProfileStore auto-save.
  - Why: most data-loss bugs come from saving on every change (throttling), from not session-locking (rollback/dupe), or from saving default data over real data after a failed load.
- BindToClose: ProfileStore handles server shutdown saves internally. For custom DataStore code, BindToClose must save all players in parallel, because the shutdown window is short (historically 30 seconds; not re-verified this session).
- Leaderboards: write to an OrderedDataStore periodically (e.g. on leave or every few minutes), not every change, and read the top N with GetSortedAsync on a timer.
- MemoryStoreService is for matchmaking queues, cross-server live leaderboards and short-lived trade locks. It expires data, so never use it for permanent saves.

### Gaps
- The exact new storage limits and whether the DataStore unification has fully shipped could not be read, because the first post of the announcement thread was inaccessible.
- MemoryStoreService quotas for 2026 were not verified.
- The ProfileStore API names (StartSessionAsync, Reconcile, EndSession, MessagingService integration) are from prior knowledge. The fetched README excerpt did not list them.

## 4. Networking and security

### Takeaway
Treat every RemoteEvent argument as hostile:
- Validate type, range and rate on the server.
- Let the server decide all outcomes: damage, currency, purchases.
- Use a typed buffer networking layer (Blink for an IDL, ByteNet/Packet for pure Luau) to cut bandwidth and centralise validation.

The biggest 2026 change is Roblox's Server Authority, generally available since July 2026. It is opt-in and uses server-authoritative physics with client prediction and rollback, blocking flings, wall clips and speed hacks for characters. New purchase handling should use MarketplaceService:BindReceiptHandler with ReceiptDecision.

### Cited Findings
- Roblox announced Server Authority (July 2026 newsroom; "[Full Release]" DevForum post). It makes the server the arbiter of game state, uses client prediction and rollback for responsiveness, and "protects from client-side cheats like flings, wall clips, or speed hacks". — [Roblox Newsroom, Jul 2026](https://about.roblox.com/newsroom/2026/07/creating-responsive-cheat-resistant-games-roblox-server-authority); [DevForum: Full Release – Server Authority](https://devforum.roblox.com/t/full-release-ship-fair-and-competitive-games-with-server-authority/4727993)
- Server Authority is opt-in. Simple games can enable character anti-cheat by turning on the prerequisites and setting `AuthorityMode = Server`. Complex custom gameplay may need rewrites using `BindToSimulation` and `InputAction`. Known caveat: "Remote events aren't synchronized with the shared timeline". Tool welds may also break on misprediction. — [DevForum: Full Release – Server Authority](https://devforum.roblox.com/t/full-release-ship-fair-and-competitive-games-with-server-authority/4727993) (search excerpt)
- Roblox's security docs start from the principle that the client cannot be trusted, and that any client-side enforcement will eventually be bypassed. — [Creator Docs: Security and cheat mitigation tactics](https://create.roblox.com/docs/scripting/security/security-tactics)
- Roblox does not provide general built-in anti-cheat APIs, so developers write game-specific checks. Opinions differ on open-source and paid anti-cheats. — [DevForum: anti-cheat APIs](https://devforum.roblox.com/t/do-you-use-anti-cheat-apis/3933116); [DevForum: anti-cheat recommendations](https://devforum.roblox.com/t/recommendations-for-robust-open-source-and-paid-anti-cheat-systems/4009996)
- UnreliableRemoteEvent payloads have a 900-byte limit in the current official reference; older mirrors say 1000 bytes. Larger payloads are dropped. Use RemoteEvent when ordering and reliability matter. Payload size is hard to measure because buffers and some types are compressed. — [Creator Docs: UnreliableRemoteEvent](https://create.roblox.com/docs/reference/engine/classes/UnreliableRemoteEvent); [robloxapi mirror](https://robloxapi.github.io/ref-temp/class/UnreliableRemoteEvent.html); [DevForum: packet dropped warnings](https://devforum.roblox.com/t/how-to-silence-packet-dropped-warnings-for-unreliableremoteevents/4042507)
- Blink is "an IDL compiler written in Luau for ROBLOX buffer networking". You write a schema and it generates typed Luau. It claims 1.6–3.7× faster than default remotes and much lower bandwidth, ships as a CLI and a Studio plugin, and the current version is 0.18.x. — [DevForum: Blink](https://devforum.roblox.com/t/blink-an-idl-compiler-written-in-luau-for-roblox-buffer-networking-0185/2959671)
- ByteNet serializes Luau data into buffers and deserializes it on the other side, with no IDL step. — [ffrostfall/ByteNet](https://github.com/ffrostfall/ByteNet)
- Packet offers more encoding choices than ByteNet (e.g. 6, 9 or 12-byte Vector3). Commenters note none of these libraries has built-in DDoS/spam protection. QuickNet is a newer drop-in alternative. — [DevForum: Packet](https://devforum.roblox.com/t/packet-networking-library/3573907?page=5); [DevForum: QuickNet](https://devforum.roblox.com/t/quicknet-v034-up-to-10x-faster-than-remoteevents-drop-in-networking-library/4624342)
- Red (red-blox) uses one remote with identifiers and packs events to save up to 75% bandwidth. The original jackdotink/Red repo is archived and moved. — [red-blox/Red](https://github.com/red-blox/Red)
- Purchases: the legacy ProcessReceipt callback can fire more than once per purchase, so record the receipt ID (idempotency) and only mark it processed after the item is granted and saved. Only one script may set ProcessReceipt. — [DevForum: Best way to use ProcessReceipt](https://devforum.roblox.com/t/best-way-to-use-processreceipt/282882); [DevForum: ProcessReceipt vs PromptProductPurchaseFinished](https://devforum.roblox.com/t/2462225)
- Newer API: `MarketplaceService:BindReceiptHandler(receiptType, callback)` with `Enum.ReceiptDecision` (Processed / NotProcessedYet). NotProcessedYet causes redelivery "during their existing session or the next time they join a server". ReceiptType covers DeveloperProduct and Robux-transfer receipts (sender and receiver). The ReceiptDecision doc page was updated 15 Oct 2026. — [Creator Docs: ReceiptDecision](https://create.roblox.com/docs/en-us/reference/engine/enums/ReceiptDecision.md); [Creator Docs: ReceiptType](https://create.roblox.com/docs/en-us/reference/engine/enums/ReceiptType.md)

### Inferences
- Common exploit types and the template defence for each:
  - **Remote spam:** a per-player, per-remote token bucket (e.g. 10 calls/sec), with drops and logging over the limit.
  - **Argument tampering:** a `typeof`/range check on every argument; reject NaN and inf numbers and Instances not owned by the player.
  - **Speed/teleport/fling:** enable Server Authority if the game fits. Otherwise use server-side distance-per-time sanity checks.
  - **Purchase spoofing:** grant only from the receipt handler, never from a client remote saying "I bought X".
  - **Damage/currency:** the client sends intent ("I swung at target T"); the server checks cooldown, range and line of sight, then applies the effect.
- For beginners, the network library choice matters less than having one module that owns all remotes and validation. Blink's schema file doubles as documentation and enforces types at runtime, which addresses the Knit author's point that types don't validate data over the wire.
- Avoid RemoteFunction server→client InvokeClient: a malicious client can yield it forever. Client→server RemoteFunctions are fine, with validation.

### Gaps
- Zap (an IDL networking compiler similar to Blink) was not found in searches, so no 2026 status is available.
- Server Authority's exact prerequisites (which workspace properties to enable), its performance cost and its mobile behaviour could not be read in full.
- I could not confirm whether ProcessReceipt is formally deprecated, or only superseded by BindReceiptHandler.

## 5. Performance

### Takeaway
Profile before optimising:
- Use the MicroProfiler (it works on mobile via a web UI) and the Developer Console's LuaHeap and InstanceCount to catch leaks.
- Tag your own code with `debug.profilebegin` and `debug.profileend`.
- The biggest wins for a template are event-driven code over per-frame loops, the `task` library, cleaning up connections with Trove, and StreamingEnabled for large maps.

### Cited Findings
- The MicroProfiler shows per-frame timing of scripts, physics and rendering. On mobile, enable it in Settings and open the web UI from a computer on the same network, which shows the last 30 frames. `debug.profilebegin` and `debug.profileend` label your own code. — [Creator Docs: MicroProfiler](https://create.roblox.com/docs/en-us/performance-optimization/microprofiler.md)
- Memory: check the Developer Console's LuaHeap first. High or growing values suggest a leak, and a rising InstanceCount is another warning sign. — [Creator Docs: Improve performance](https://create.roblox.com/docs/en-us/performance-optimization/improve)
- A Studio Beta "LibMP" MicroProfiler API exists for live profiling. Enabling the MicroProfiler raises memory use, so enable it only for a fraction of sessions. — [DevForum: LibMP](https://devforum.roblox.com/t/studio-beta-introducing-libmp-the-microprofiler-api/4703136)

### Inferences
- Template rules:
  - Use `task.wait`, `task.spawn` and `task.delay`; the old `wait()`, `spawn()` and `delay()` are deprecated, throttled and legacy.
  - One shared Heartbeat/RenderStepped loop per system, never one per object.
  - Disconnect everything through a Trove, especially on character respawn and UI close.
  - Pool frequently created objects such as projectiles and effects.
- Parallel Luau (Actors with `task.desynchronize`) helps only for heavy, independent computation such as pathfinding batches or procedural generation. It adds complexity, so it doesn't belong in a beginner template by default.
- StreamingEnabled is on by default for new places and is essential on low-end mobile. Code must expect parts to be missing on the client (use `WaitForChild` with a timeout, or CollectionService instance-added signals).

### Gaps
- Official mobile memory budgets for 2026 and Parallel Luau/Actor guidance pages could not be fetched. No concrete numbers are available.
- I could not verify a dedicated "ScriptProfiler" doc beyond MicroProfiler references.

## 6. Testing and publishing workflow

### Takeaway
TestEZ is archived. Jest-Lua (jsdotlua) is the maintained Roblox test framework. Roblox's Open Cloud Luau Execution API allows headless test runs against a specific place version in CI, and Roblox publishes a reference repo (place-ci-cd-demo) combining Rojo and Luau Execution. Use separate dev, test and prod places, publishing to prod only from CI or a single person.

### Cited Findings
- Open Cloud Luau Execution runs Luau headlessly in a place. A listed use case is "automated testing: run test scripts against specific place versions as part of a CI/CD pipeline". Tasks run up to 5 minutes, with at most 10 concurrent tasks per place. The reference implementation is Roblox/place-ci-cd-demo (Rojo plus Luau Execution). — [Creator Docs: Luau Execution](https://create.roblox.com/docs/en-us/cloud/reference/features/luau-execution.md)
- Jest Lua (jsdotlua) is a Luau port of Jest, aligned to Jest v27.4.7. It "can currently only run inside of Roblox", and the latest listed version is 3.10.0 (Oct 2024). TestEZ is archived. — [jest-environment-roblox package](https://classic.yarnpkg.com/en/package/@jsdotlua/jest-environment-roblox); [Roblox GitHub org](https://github.com/roblox)
- jest-roblox-cli (community) offers Open Cloud and Studio backends and GitHub Actions output formatting. Its maturity is unverified. — [jest-roblox-cli CONTRIBUTING](https://raw.githubusercontent.com/christopher-buss/jest-roblox-cli/HEAD/CONTRIBUTING.md)
- The Studio MCP server can start and stop playtests and read console output, which enables AI-driven playtest smoke tests. — [MoguraVR](https://www.moguravr.com/roblox-studio-mcp-server-agentic-update/)

### Inferences
- Workflow:
  1. One experience with a "Dev" place, or a separate private Dev experience, and a "Staging" experience mirroring prod with a separate DataStore scope or name prefix (e.g. `PlayerData_DEV`), so testers never touch real saves.
  2. CI on each merge to main: Selene, StyLua check, luau-lsp/`luau-analyze` type check, Jest tests via Luau Execution, then a rojo build and publish to Staging.
  3. Publish to prod by manual approval.
  4. Rollback through place version history.
- Unit-test pure modules (migrations, economy maths, validators) first. They are cheap to test and the most damaging to get wrong.

### Gaps
- Current Jest-Lua release status in 2026 is unknown; the last seen changelog was from 2024.
- No 2026 official doc on "staging places" best practice was found; the workflow above is inferred.

## 7. Reusable modules for a personal template

### Takeaway
Keep the template small: a loader, a typed network module, a DataService (ProfileStore), a PurchaseService (BindReceiptHandler with receipt idempotency), Signal, Trove, a simple UI state store, a SoundController, and an analytics wrapper. Prefer well-known Wally packages (Sleitnick's signal and trove) over home-grown versions.

### Cited Findings
- Sleitnick's Signal and Trove are published on Wally (example manifest lines `sleitnick/signal@2.0.0` and `sleitnick/trove@1.1.0`; check the index for current versions). Trove handles lifecycle and cleanup of connections and instances. — [roblox-game-skill tooling reference](https://mintlify.wiki/brockmartin/roblox-game-skill/reference/tooling-ecosystem); [RbxUtil docs index](https://docsearch.algolia.com/mcp/docs/repo/sleitnick/rbxutil)
- ProfileStore is a single ModuleScript, suitable as the base of a datastore wrapper. — [MadStudioRoblox/ProfileStore](https://github.com/MadStudioRoblox/ProfileStore)
- Purchase handler requirements: idempotent receipt handling and a single handler per game. — [DevForum: Best way to use ProcessReceipt](https://devforum.roblox.com/t/best-way-to-use-processreceipt/282882); [Creator Docs: ReceiptDecision](https://create.roblox.com/docs/en-us/reference/engine/enums/ReceiptDecision.md)

### Inferences
- Suggested template contents and why each matters:
  - **Loader** (Init/Start): predictable startup and no circular-require surprises.
  - **Net** (Blink schema or a thin RemoteEvent wrapper with validators and rate limiting): one place to secure.
  - **DataService:** defaults, migrations, ProfileStore and leaderstats sync, so the riskiest code (saves) is written once and tested.
  - **PurchaseService:** a product-ID → grant-function table. It writes the receipt ID into the profile before returning Processed.
  - **Signal and Trove:** event plumbing and leak-free cleanup.
  - **UIController/state:** a plain table store with a Changed signal. Use a UI library such as React-Lua or Fusion only if the team already knows it.
  - **SoundController:** pooled sounds and volume categories.
  - **AnalyticsService wrapper:** a thin layer over Roblox AnalyticsService custom and economy events, so every game logs the same funnel.
  - **Config:** constants in ReplicatedStorage/Shared.
- Keep each module under about 300 lines with `--!strict` and a short header comment. AI assistants and new team members both work better with small, typed modules.

### Gaps
- No verified 2026 source for Fusion vs React-Lua adoption, or for AnalyticsService API changes.
- No authoritative "official template" from Roblox was found. Community templates such as jecs-template exist but are ECS-specific.
