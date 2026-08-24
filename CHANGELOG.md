# Changelog

All notable changes to this project will be documented in this file.

This project follows semantic versioning while it is in early development.

Both `managed-deepagents` runtime packages (npm and PyPI) publish together at the
same version. Changelog entries still call out which surface a change landed in
(`npm`, `pypi`, and/or `cli`) when that distinction is useful.

On each non-dev release, notes are generated from git commits since the previous
`vX.Y.Z` tag (conventional `feat` / `fix` / …). Optional curated bullets under
`## Unreleased` are merged in first.

## Unreleased

## 0.6.0 - 2026-08-24

### Added

- Generate Slack icons from app names (`cli`) (#381)
- Add Slack app background color [CLOSES AB-000] (`fleet`) (#379)
- Log Trigger channel traffic (`channels`) (#369)
- Support custom Slack channel icons (`mda`) (#372)
- Scaffold Slack from mda init --channel (`cli`) (#371)
- Warn when channel/ is used instead of channels/ (`cli`) (#370)
- Standardize guidance output sequences (`cli`) (#373)
- Guide slack responses with mrkdwn (`sdk`) (#365)
- Define analytics event contract (`cli`) (#359)
- Add Slack channel init command (`cli`) (#364)
- Add Harbor evaluation workflow (`evals`) (#351)
- Identify HTTP requests with User-Agent (`cli`) (#357)
- Prototype Trigger-backed Slack channels [closes LSD-1857] (`sdk`) (#348)
- Bake setup.sh into a recipe snapshot at deploy (`sandbox`) (#339)
- Introduce interactive init mode (`cli`) (#349)

### Changed

- Bump uuid in the minor-and-patch group (`deps`) (#386)
- Bump oxc from 0.144.0 to 0.146.0 in the major group (`deps`) (#387)
- Bump oxfmt (`deps-dev`) (#388)
- Bump the minor-and-patch group (`deps-dev`) (#389)
- Update npm dependencies (`security`) (#368)
- Pin LangGraph API image to stable 0.12.6 (#350)
- Remove LANGSMITH_GATEWAY_API_KEY preflight requirement (#347)

### Fixed

- Fail deploy when sandboxes are disabled for the org (`cli`) (#391)
- Make slack app metadata optional (`channels`) (#390)
- Send interrupt envelopes on run.interrupted (`channels`) (#383)
- Emit run.interrupted and accept interrupt_resume (`channels`) (#380)
- Skip recipe snapshots still used by sandboxes (`cli`) (#377)
- Normalize authored assistant ids (`sdk`) (#376)
- Pause deploy for Slack authorization (`fleet`) (#366)
- Avoid redundant Python dev reloads (`cli`) (#358)
- Show install-specific docs link (`cli`) (#362)
- Require Gateway provider keys (`sdk`) (#352)
- Improve missing Slack channel error (`cli`) (#346)
- Sync Python lockfile metadata (`release`) (#345)
## 0.5.3 - 2026-08-18

### Added

- **npm:** Ship ambient `*.md` typings via the package `"types"` entry
  (`types/markdown-md.d.ts`) so `import prompt from "./file.md" with { type: "text" }`
  type-checks without a project-local `declare module "*.md"` (matches MDA's
  compile-time text-module inlining for schedule prompts and similar).
- Upsell a plan upgrade when the org lacks the entitlement (`deploy`) (#274)
- Improve mda init onboarding experience [closes LSD-1863] (`cli`) (#338)
- Support LangSmith Gateway provider (`models`) (#336)
- Remove credentials authoring and runtime overlay (`identity`) (#322)
- Ship ambient *.md typings for text-module imports (`npm`) (#306)
- Watch project sources and reload in mda dev (`cli`) (#300)

### Changed

- **cli, breaking:** `mda deploy` no longer reads deployment secrets from the
  process environment. A provider key, gateway key, ingress secret, or connector /
  channel secret is now taken only from the project `.env` or LangSmith workspace
  secrets. Previously a value exported in your shell was copied out and uploaded as
  a persisted deployment secret, so an `OPENAI_API_KEY` set in a shell profile for
  unrelated local work silently became long-lived credential material on the
  deployment. Deploys that relied on the shell now fail with guidance; move the key
  into `.env` or add it under Settings → Workspaces → Secrets.
- Remove leftover custom-credentials authoring and runtime overlay: `defineIdentity`
  / `define_identity` reject `credentials`, the `credentials` namespace
  (`credentials.github`) is gone, and tools no longer receive `runtime.credentials`.
  Use env tokens (for example `GITHUB_TOKEN`) in authored tools (`npm`, `pypi`).
- **cli:** Inline only `with { type: "text" }` text-module imports. The
  undocumented `type: "markdown"` alias is no longer accepted.
- Remove Connect-with-X leftovers after that surface was deleted (`npm`, `pypi`,
  `cli`):
  - Drop `/identity/{provider}/callback` auth bypass and `/identity` CORS
    allowlisting (no identity HTTP routes remain).
  - Stop injecting or documenting `MDA_GUEST_SIGNING_KEY` (OAuth `state` signing
    had no remaining readers).
  - Keep the `mda_github_credentials` store ACL reserved (no Connect writers
    remain; leftover tokens must stay unreadable until scrubbed).
  - Remove empty `repoPrefix` mount branches that existed only for per-user Hub
    roots.
  - Stop vendoring a nonexistent `./evals` package export and stop injecting the
    unused `uuid` TypeScript dependency.
  - Delete orphaned Python extractors (`name.py`, `ingress.py`) and refresh
    Connect / per-user memory wording in READMEs, init scaffolds, and examples.
- **integration-tests:** Restore `COVERAGE.md`, re-enable
  `channels-skip-non-exports.standalone.test.ts`, and delete unused
  `evals/scaffold/{contracts,harbor-custom,identity,overlays}` trees that no
  test referenced.
- Guard Context Hub edits during deploy (#257)
- Stop reading deployment secrets from the process environment (`cli`) (#340)
- Bump cliclack (`deps`) (#329)
- Bump the major group across 1 directory with 2 updates (`deps`) (#333)
- Bump the minor-and-patch group across 1 directory with 6 updates (`deps`) (#334)
- Bump the minor-and-patch group (`deps`) (#332)
- Update nanoid to 3.3.18 (`deps`) (#308)

### Fixed

- Honor `default_tool_timeout` on Python HTTP/SSE MCP connectors instead of
  forwarding it into the adapter session constructor and crashing `mda dev`
  (`pypi`). Non-positive timeouts are now rejected in both runtimes (`npm`,
  `pypi`).
- Default dev traces to assistant project (`cli`) (#337)
- Omit redundant current-directory paths (`cli`) (#328)
- Require audience for JWKS tokens (`identity`) (#324)
- Use the project venv for Python connector emit (`cli`) (#315)
- Keep Slack manifest URL selectable (`sdk`) (#319)
- Say Slack manifest template was created (`cli`) (#316)
- Stop HTTP MCP from crashing on default_tool_timeout (`pypi`) (#317)
- Float TypeScript LangChain dependencies (`compile`) (#271)
- Use uv for Python deploy emit [closes LSD-1814] (#299)
## 0.5.2 - 2026-08-11

### Changed

- Bump the minor-and-patch group (`deps-dev`) (#297)
- Bump the minor-and-patch group (`deps`) (#296)
- Bump the minor-and-patch group with 2 updates (`deps`) (#295)
- Bump Swatinem/rust-cache in the minor-and-patch group (`deps`) (#294)
- Fix Python sandbox timeout serialization (#292)
- Bump npm langsmith to ^0.8.9 (#290)
- Bump oxc from 0.142.0 to 0.143.0 in the major group across 1 directory (`deps`) (#250)
- Bump deepagents (`deps`) (#285)
- Bump the npm_and_yarn group across 3 directories with 2 updates (`deps`) (#284)
- Bump the npm_and_yarn group across 3 directories with 1 update (`deps`) (#268)
## 0.5.1 - 2026-08-08

### Added

- Revive MCP connector (#262)

### Changed

- Update python deps (#283)
## 0.5.0 - 2026-08-07

### Added

- `auth.langsmithApiKey()` / `auth.langsmith_api_key()` explicitly enables
  `x-api-key` ingress while retaining MDA's thread and store authorization
  callbacks. The managed runtime verifies keys against the platform-owned
  LangSmith auth endpoint, enforces the deployment tenant, and maps accepted
  keys to scoped service identities (`npm`, `pypi`, `cli`).
- Identity declarations now require an explicit `auth` selection. `mda init`
  scaffolds LangSmith API-key authentication by default in both languages;
  argument-free `defineIdentity()` / `define_identity()` declarations fail
  during authoring and compilation (`npm`, `pypi`, `cli`).
- `mda init <name> --gateway` scaffolds a project that runs on LangSmith Gateway
  (`cli`). The agent file constructs an OpenAI-compatible client against
  `https://gateway.smith.langchain.com/v1` on a model LangSmith hosts, billed to
  the workspace's Gateway Credits, and authenticates with a LangSmith API key
  read from `LANGSMITH_GATEWAY_API_KEY` — `LANGSMITH_API_KEY` is reserved and
  never reaches a deployment, so `.env` is seeded under both names. Because the
  model is constructed rather than named as a `provider:model` string, deploy
  pre-flights no provider key. Mutually exclusive with `--model`.
- `mda deploy` now pre-flights `LANGSMITH_GATEWAY_API_KEY` for a project whose
  agent runs on LangSmith Gateway (`cli`), the same way it already pre-flights a
  model provider key: blocked only when the key is confirmed absent from `.env`,
  the process environment, and LangSmith workspace secrets. Previously a project
  scaffolded with `--gateway` but no key set deployed cleanly and failed on its
  first message with an opaque gateway 401.
- `mda delete` (alias `mda destroy`) tears down a deployment's LangSmith
  resources: the deployment, its tracing project, its Context Hub repo including
  per-user memory and legacy child repos beneath it, and the managed sandboxes it
  created. Confirms before deleting unless `--yes` is passed (`cli`)
- Managed sandboxes are now named `{deployment}--{digest}` so they can be
  attributed to the deployment that created them. `mda deploy` passes the
  deployment name to the runtime as `MDA_DEPLOYMENT_NAME` (`cli`, `npm`, `pypi`)
- `mda logs` reads a deployed agent's Agent Server logs. In a terminal it
  streams until Ctrl-C; piped or redirected it prints the most recent lines
  (1000 by default, `--lines`) and exits. Also supports `--level`,
  `-f`/`--no-follow`, and `--tenant-id` (`cli`)
- In a terminal, `mda init` prompts for a missing project name. Adding
  `--interactive` / `-i` also offers a coding-agent handoff after scaffolding.
  `mda init <name>` remains non-interactive for scripts and coding agents, and
  default completion prints language-specific quickstart and deploy steps (`cli`)
- `mda init` takes the project's shape as flags, so a coding agent or a CI
  script can scaffold a specific project without answering prompts:
  `--instructions`/`--instructions-file` (`-` reads stdin) for
  `instructions.md`, `--scope <boundary>` for an identity declaration,
  `--model` for the agent's model, and `--no-sandbox`/`--no-evals` to leave
  those out. The generated README describes whatever was scaffolded (`cli`)
- `identity.credentials` accepts a map keyed by target name, so one deployment
  can integrate several platforms without hand-writing the dispatch. Each entry
  keeps declaring its own Connect-with-X routes, which a hand-written wrapper
  would have hidden (`npm`, `pypi`)
- Connect-with-X routes are inferred from the rest of the identity declaration:
  GitHub when a credential chain reads user tokens on a user-scoped deployment,
  Slack when a Slack channel is declared on one. `connect` remains for custom
  providers (`npm`, `pypi`)
- Slack Events uses a **bring-your-own Slack app**: put `SLACK_SIGNING_SECRET`
  and `SLACK_BOT_TOKEN` in `.env` (deploy preflights them via
  `SLACK_CHANNEL_REQUIRED_ENV`), point Slack Event Subscriptions at
  `/connectors/{name}/events`, and subscribe to the bot events implied by `on`.
  Fleet/LangSmith no longer provisions the bot app; the optional authoring
  `app` branding bag and deploy-owned secret strip are gone (`cli`, `npm`,
  `pypi`)
- Default identity to LangSmith API key auth
- Add `mda init --gateway` (`cli`) (#255)
- Scaffold identity on init (`cli`)
- Create a default Slack manifest template
- Add Slack channel manifest command
- Generate Slack app manifests during deploy
- Remove guest ingress entirely (`identity`)
- Remove auth.guest from the public authoring surface (`identity`)
- State memory instructions at runtime, not in the memory file (`memory`)
- Declare durable memory in memory.{ts,py}, off by default (`memory`)
- Make eval task workflow explicit (`cli`)
- Personalize Slack Events via Connect-with-Slack (`channels`)
- Invoke Slack Events as mda:slack agent principal (`channels`)
- Put Slack Events on channels.slack (`channels`)
- Drop unused threads, partition, and access axes (`identity`) (#220)
- Require bring-your-own Slack app secrets (`slack`) (#218)
- Require confirmation for resource collisions
- Remove organization identity from MDA (#213)
- Slice-based user and agent memory (`identity`) (#210)
- Warn on first-deploy resource collisions
- Opt into langgraph-api version via env (`cli`) (#198)
- Thread LANGSMITH_ENDPOINT into device login (`cli`)
- Enable login auth flow for deploy and connect (`cli`) (#191)
- Add mda connect for OAuth and workspace API keys (`cli`) (#190)
- Add Fleet marketplace MCP bridges and LinkedIn Connect (`connectors`) (#189)
- Connect Google per actor and provision Slack in mda dev (`identity`) (#181)
- Fold channels into connectors (`connectors`) (#177)
- Create a channel's Slack app through LangSmith (`channels`) (#176)
- Reach every LangSmith tool server integration (`connectors`) (#175)
- Add onboarding TUI (`cli`) (#158)
- Add mda logs and print the Agent Server URL on deploy (`cli`) (#160)
- Add mda delete and clean up the sandboxes it created (`cli`) (#159)

### Changed

- `mda init` now scaffolds the required `identity.ts` or `identity.py`
  declaration by default. The redundant `--identity` flag is
   removed; both it and the previously retired `--scope` flag are rejected
   (`cli`).
- A first `mda deploy` now asks for confirmation before overwriting a same-name
  resource it does not own: a Context Hub repo created outside `mda deploy`, or
  a non-MDA LangSmith deployment. It fails closed in non-interactive terminals.
  Deploy-owned resources are recognized by the `managed-deepagents` repo tag and
  the deployment's Managed Deep Agent marker, so redeploys — and retries after a
  deploy that failed partway — are never prompted (`cli`)
- `mda deploy` now prints the Agent Server URL next to the dashboard link on
  success, so there is a URL to call without opening LangSmith (`cli`)
- A restarted or redeployed container now re-adopts its existing sandbox for the
  same scope instead of creating a replacement and stranding the old one until
  its idle TTL expires. The sandbox name digests how it was provisioned, so
  changing `setup.sh` or the snapshot still gets a fresh sandbox; only a sandbox
  built from the same recipe is adopted, and adopting one skips `setup.sh`
  (`npm`, `pypi`)
- Fix required Harbor task staging files (#278)
- Fix repository format and lint checks
- fix Rust tests after main merge
- fix Python checks after main merge
- fix loopback auth and CI after main merge
- add changes
- Move eval scaffolds under evals workspace
- Make sandbox definitions backend neutral
- Expose sandbox definition factories
- Clarify API key auth resolution
- adding api key auth
- Enable Slack app direct messages
- Remove init identity flag (`cli`)
- Source Slack app settings from template
- Bump the minor-and-patch group (`deps`) (#251)
- Bump the minor-and-patch group (`deps-dev`) (#252)
- Bump clap from 4.6.4 to 4.6.5 in the minor-and-patch group (`deps`) (#249)
- breaking(identity): expose only Supabase auth
- fix Slack test formatting
- breaking(identity): remove x-mda-groups header
- breaking(identity): remove the auth.github() provider
- Preserve custom Harbor tasks during eval compilation
- breaking(channels): drop `on` from channels.slack (#230)
- chore/remove-scopes-from-interface
- Drop the migration for memory files older deploys already have (`memory`)
- Remove per-caller memory, and stop the store gate depending on it (`memory`)
- Drop comments the code already states (`cli`)
- Update standalone eval staging assertions
- Bump cryptography from 49.0.0 to 50.0.0 in /packages/pypi (`deps`)
- Simplify MDA eval task scaffolding
- change evals
- git ignore
- Bump ip-address from 10.2.0 to 10.4.0 in /packages/npm (`deps`) (#206)
- Bump fast-uri from 3.1.4 to 3.1.5 in /packages/npm (`deps`) (#203)
- Bump postcss from 8.5.22 to 8.5.25 in /packages/npm (`deps-dev`) (#202)
- Bump @hono/node-server in /packages/npm (`deps`) (#205)
- Bump hono from 4.12.32 to 4.13.0 in /packages/npm (`deps`) (#207)
- Bump @hono/node-server and @modelcontextprotocol/sdk (`deps`) (#201)
- Default `defineIdentity` scope to agent (`identity`) (#196)
- Rename organizations to organization (`identity`) (#197)
- Clean up high-priority Rust duplication and inefficiency (`cli`) (#195)
- Clean up runtime duplication and async Connect-hint I/O (`pypi`) (#193)
- Dedupe Connect OAuth helpers and drop marketplace wrap (`npm`) (#192)
- Replace LANGCHAIN_* env vars with LANGSMITH_* (`cli`) (#194)
- Bump deepagents (`deps`) (#186)
- Bump pypa/gh-action-pypi-publish (`deps`) (#185)
- Bump base64 from 0.22.1 to 0.23.0 in the major group (`deps`) (#187)
- Reach every provider as <primitive>.<provider>() (`primitives`) (#173)
- Bump oxc from 0.141.0 to 0.142.0 in the major group (`deps`) (#169)
- Bump ty in /packages/pypi in the minor-and-patch group (`deps-dev`) (#171)
- Move compile's tests out of compile/mod.rs, colocating where a stage owns them (`mda`) (#161)
- Scope workspace via --workspace-id (`deploy`) (#147)
- Bump the minor-and-patch group in /packages/npm with 3 updates (`deps`) (#156)
- Bump the minor-and-patch group in /packages/pypi with 3 updates (`deps-dev`) (#157)
- Bump the minor-and-patch group across 1 directory with 4 updates (`deps`) (#153)
- Bump actions/setup-python in the major group (`deps`) (#154)
- Bump fast-uri from 3.1.3 to 3.1.4 in /packages/npm (`deps`) (#149)
- Bump the minor-and-patch group with 2 updates (`deps`) (#152)
- Bump oxc from 0.140.0 to 0.141.0 in the major group (`deps`) (#155)
- Bump the npm_and_yarn group across 4 directories with 3 updates (`deps`)
- Bump the npm_and_yarn group across 2 directories with 2 updates (`deps`)
- fix hot memory integration marker
- fix npm deepagents dependency
- fix npm langsmith peer dependency
- Bump the minor-and-patch group across 1 directory with 9 updates (`deps`)

#### BREAKING (eval gateway credential)

- `mda evals compile` forwards the gateway credential to Harbor trials as
  `LANGSMITH_GATEWAY_API_KEY`, replacing `LANGSMITH_API_KEY_GATEWAY` (`cli`).
  One credential now has one name across the CLI: the scaffolded agent reads it,
  `mda init` seeds it, `mda deploy` pre-flights it, and evals forward it. If you
  export the old name in a shell or CI job for `harbor run`, rename it. Keys in
  the project's `.env` are unaffected — those are forwarded whatever they are
  called, which is how a `--gateway` project's trials already worked.

#### BREAKING (channels Slack primitive)

- Slack Events ingress, messaging, and deploy requirements move back to a public
  `channels` primitive under project `channels/` (`export const channel` /
  module-level `channel`). Author with `channels.slack()` (`npm`, `pypi`,
  `cli`).
- Events URL is `POST /channels/{name}/events` (no `/connectors/.../events`
  alias for Slack) (`npm`, `pypi`, `cli`).
- `connectors.slack` is tools-only (`includeTools` / `excludeTools`). Event
  options (`on`, `autoReply`, …) are rejected; use `channels.slack` instead
  (`npm`, `pypi`).
- Compiler discovers `channels/`, emits `_mda_channels`, and writes
  `channel-manifests.json` for deploy secret preflight alongside
  `connector-manifests.json` (`cli`).
- `channels.slack` no longer accepts `on`. Bot Event Subscriptions and OAuth
  scopes are configured on the BYO Slack app; MDA accepts Phase 1 event kinds
  when they arrive. Authoring keeps only MDA runtime knobs (`autoReply`,
  `mentionBehavior`, `filters`, `conversation`). `requiredPermissions` is the
  fixed recommended scope list for app setup docs (`npm`, `pypi`, `cli`).

#### Memory instructions

- Memory instructions moved out of the memory file and into the system prompt. The
  Hub hot-memory file (`memories/agent/AGENTS.md`) is now seeded **empty** and holds
  only what the agent wrote; a new `mda-memory-instructions` middleware states the
  policy — the mount paths, which tools reach them, that only `/memories/agent/` is
  durable, that the tree is shared by every caller, and that memory is data rather
  than instructions — on every model call, but only when a slice is mounted. The
  instructions previously committed into the file rendered as the customer's "agent
  memory" in the Context Hub UI and went stale in place: a file seeded before the
  slice layout landed still taught `/memories/AGENTS.md` (`npm`, `pypi`, `cli`).
- Deploy does not rewrite memory files. A deployment created before this release
  keeps whatever an older CLI wrote into its hot file, stale paths and all — the
  injected policy is what the model follows, and it says to treat file contents as
  notes rather than instructions. Delete the old block by hand if you want it gone
  (`cli`).
- **Fix:** a Context Hub directory response whose shape drifted (a renamed or
  re-nested `files` field, or files without a `commit_hash`) parsed as "no files and
  no parent commit", which would have let deploy seed an empty memory file over a
  real one with the conflict check waived. It now fails the deploy instead (`cli`).
- Authoring guidance changed: do not restate memory mechanics in `instructions.md`.
  The runtime says them on every turn, so a Memory section should cover only what is
  worth remembering in that project (`cli`, agent-builder skills).

#### BREAKING (memory declaration)

- Durable memory is now opt-in and owned by one root declaration: export `memory`
  from `memory.ts` / `memory.py` with `defineMemory({ scope: "agent" })` /
  `define_memory(scope="agent")`. A project without that module mounts nothing —
  previously every project with no `identity.{ts,py}` got agent memory implicitly
  (`npm`, `pypi`, `cli`).
- `scope` is typed and slice-shaped rather than a boolean: `"agent"`, `"none"`,
  or `["agent"]` today. `"user"`, object slices (`{ kind, mount, access }`),
  `partition`, `access`, `mount`, `retention`, `provider`, and
  `sleepTimeCompute` are rejected with errors that name them as not-yet-supported,
  so later slice kinds land as data in the same shape (`npm`, `pypi`).
- `disableMemory` / `disable_memory` on the agent definition is removed and now
  fails the build for **any** value: `false` used to mean "memory on", so
  honoring it under an opt-in contract would invert what was written. Delete it —
  memory is already off unless declared (`npm`, `pypi`, `cli`).
- `scope.memory` on `defineIdentity` / `define_identity` is removed and fails the
  build with a migration message. Identity says who is calling; memory says which
  slices exist. `scope: "user"` keeps its threads/credentials meaning and no
  longer implies memory, and `IdentityConfig["scope"]` no longer carries a
  `memory` axis (`npm`, `pypi`, `cli`).
- Per-caller memory is **removed**, not just unauthorable: the `/memories/user/`
  mounts, the per-user Context Hub repo (`{deploy}--u--{user}`), the lazy per-run
  remount (`LazyPerRunContextBackend`), the per-user hot-memory seeding, and the
  user-slice helpers are gone from both runtimes. `ResolvedMemorySlice` is
  agent-only, so a future private slice is rebuilt rather than re-enabled. The
  resolved config stays a versioned slice list, so adding a kind later does not
  change what consumers read. `mda delete` still tears down legacy `--u--` child
  repos, because deployments made before this release still have them
  (`npm`, `pypi`).
- **Security:** the store authorization gate no longer depends on memory. The
  reserved managed tables (`mda_identity_links`, `mda_github_credentials` — account
  links and OAuth tokens for every caller) were checked *after* a per-caller memory
  check that returned early whenever no user slice was declared, so on any
  deployment without one — every deployment, in this release — an authenticated
  caller could read or overwrite other callers' entries. The reserved-table check
  now runs first and unconditionally, and `buildManagedAuth` /
  `build_managed_auth` no longer take a memory declaration (`npm`, `pypi`, `cli`).
  Reported by Corridor on #229.
- A memory `scope` that is not a static literal fails the build: deploy seeds the
  hot file from that value, so it cannot be decided at runtime (`cli`).
- The shared slice is documented as a trust boundary. Hot memory is injected into
  every run and ordinary runs can write it, so one caller can persist content —
  including instructions — that every later caller reads. The launch mount stays
  read/write; the seeded `AGENTS.md` now tells the model that memory is recorded
  data rather than orders and cannot widen what it may do, and the authoring
  helpers, scaffolded templates, and builder skill say who should not enable it. A
  privileged-writer policy is future work (`npm`, `pypi`, `cli`).
- `mda init --memory <agent|none>` scaffolds the declaration; without the flag no
  memory module is written. `mda dev` seeds `.mda/__contexthub__/memories/agent/`
  only when memory is declared, and deploy warns when Context Hub already holds
  memory files a project no longer declares (they are preserved, not deleted)
  (`cli`).

#### BREAKING (identity scopes)

- Organization-scoped identity is removed. `scope: "organization"`, the
  `organization` authoring option / requirement, organization claim mappings,
  organization fields on `runtime.identity`, and user-memory
  `partition: "organization"` are rejected. Trusted ingress no longer accepts
  `x-mda-organization-id` as an identity field (the header and
  `mda_organization_id` stay reserved so request bodies cannot spoof them).
  Private memory is always `{deploy}--u--{user}`; the CLI still deletes legacy
  `--t--` Hub children during teardown (`npm`, `pypi`, `cli`).
- The `conversation` thread scope and `mda init --scope shared-conversations`
  preset are removed. Threads are always user-owned; the `scope.threads`
  authoring/resolved axis and the `ThreadScope` type are gone. Shared-bot
  recipes use user-owned threads and memory, with `credentials: "agent"` when
  they need the shared vault (`npm`, `pypi`, `cli`).
- User-memory `partition` is gone from the resolved slice shape. User memory is
  always per-caller keyed; omit `partition` on `{ kind: "user" }` (any value,
  including `"user"`, is rejected). The `MemoryPartition` type and
  `userMemoryPartition` / `user_memory_partition` helpers are removed
  (`npm`, `pypi`).
- Memory slice `access` (`"rw" | "ro"`) and the `MemoryAccess` type are removed.
  Mounts are always read/write; omit `access` on slice objects (`npm`, `pypi`).
- Authoring `scope.memory` slices are string shorthands only (`"user"` /
  `"agent"`). Object form (`{ kind }`) is rejected until there are real
  per-slice options; resolved config still uses `{ kind }` (`npm`, `pypi`).
- `defineIdentity()` / `define_identity()` now default to `scope: "agent"`
  (shared memory + LangSmith vault) instead of `"user"`. Per-caller Connect
  needs an explicit `scope: "user"`. `mda init --scope agent` scaffolds the
  argument-free declaration; `--scope user` writes the scope explicitly
  (`npm`, `pypi`, `cli`).
- Override bags with no `default` also inherit `"agent"`.
- Fleet tool errors on agent-scoped / no-identity deployments point at
  `mda connect` / LangSmith Integrations instead of Connect-with-X
  (`npm`, `pypi`).

#### BREAKING (primitive authoring surface)

Every primitive that has more than one provider is now selected as
`<primitive>.<provider>(…)` from a first-party namespace, and the old authoring
names were removed rather than deprecated. Nothing has shipped to users, so
there is no migration window. `specification/primitives/` has the design;
`docs/` has the contributor guides.

**Authoring** (`npm`, `pypi`)

| Was                                                     | Now                                              |
| ------------------------------------------------------- | ------------------------------------------------ |
| `defineSlackChannel` / `define_slack_channel`           | `connectors.slack`                               |
| `defineGitHubChannel` / `define_github_channel`         | removed (use custom tools + `credentials.github`) |
| `channels.slack` / `channels.github`                    | `connectors.slack` / removed                      |
| `defineMcpServers` / `define_mcp_servers`               | `connectors.mcp`                                 |
| `github.connector`                                      | removed                                          |
| `langsmith.connector` / `connectors.langsmith`          | removed (see above)                              |
| `sandboxes.langsmith(…)`                               | `defineSandbox(…)` / `define_sandbox(…)`         |
| `providers.*`                                           | `auth.*`                                         |
| `github.credentials(…)`                                 | `credentials.github(…)`                          |
| `github.connect()` / `slack.connect()`                  | `connect.github()` / `connect.slack()`           |
| `channels/` directory + `export const channel`          | `connectors/` + `export const connector`         |
| `POST /channels/{name}/events`                          | `POST /connectors/{name}/events`                 |
| GitHub channel `handlers`                               | removed (custom tools + `credentials.github`)    |

- **Channels → connectors (BREAKING):** the public `channels` namespace and
  `channels/` project directory are gone. Slack Events and messaging declare
  under `connectors/` with `export const connector` / `connector =`. Events URLs
  are `/connectors/{name}/events`.
- `defineSandbox(…)` / `define_sandbox(…)` implicitly select LangSmith, so a
  project does not import `LangSmithSandbox` from `deepagents`. MDA still
  supports only that backend; a backend selector can be added if more are
  supported later.
- Connector modules under `connectors/` export a `connector` in both languages
  — `export const connector = connectors.mcp(…)` in TypeScript, a module-level
  `connector = …` in Python. The earlier named `mcp` export is gone, and a
  TypeScript `export default` is now a build error naming the fix rather than a
  module the compiler skips in silence.
- Python's internal connector/channel implementation packages are `_connectors`
  and `_channels` (runtime helpers), so they do not shadow the public
  `connectors` namespace.

**Contribution API** (`npm`, `pypi`)

- The primitives are now built on one internal `defineExtension(kind, options)`
  (`define_extension` in Python), narrowed by kind for `channel`, `connector`,
  and `sandbox`. Each declares its input as `args`: any
  [Standard Schema](https://standardschema.dev) (Zod, Valibot, ArkType) or a
  plain function in TypeScript, and a pydantic model / `TypeAdapter` — anything
  exposing `model_validate` or `validate_python` — or a callable in Python.
  Both runtimes validate through those interfaces, so a contributor can bring
  their own library.
- The first-party primitives now validate with schemas — Zod in the npm package,
  pydantic in the PyPI package — instead of hand-written checks. `zod` is a
  dependency of `managed-deepagents` (npm) and `pydantic>=2` of
  `managed-deepagents` (PyPI), which previously had no runtime dependencies.
  Validation errors now name the failing path (`mcpServers.docs.url`) and read
  slightly differently for plain type mismatches, which Zod and pydantic word
  themselves; the messages for MDA's own rules are unchanged in substance.
- It is **not exported**, and neither are the extension points it replaces:
  `defineChannel` and the `managed-deepagents/channels` subpath are gone, and
  the connector brand and hook context types now live only on
  `managed-deepagents/runtime`. A project selects primitives from the
  first-party namespaces and cannot mount an adapter, HTTP route, or sandbox
  backend of its own.

#### BREAKING (identity)

The identity surface was reworked and the old spellings were removed outright
rather than deprecated, since nothing has shipped to users yet. Everything below
is a rename or a removal; no capability was dropped.

**Authoring — `identity.ts` / `identity.py`** (`npm`, `pypi`)

- `defineIdentity` / `define_identity` no longer accept the
  `{ ingress, tenancy, scoping }` config. Declare `auth`, `scope`, `credentials`,
  and `connect` instead; unknown keys now throw.
- `defineIdentity.preset(...)` / `define_identity.preset(...)` are removed, along
  with the `IdentityPresetName` type. `private-assistant` and `internal-tool`
  become `defineIdentity()` (they were identical in behavior), shared bots use
  `defineIdentity({ scope: { memory: "user", credentials: "agent" } })`,
  multi-tenant apps use per-user isolation, and `service` becomes
  `defineIdentity({ scope: "agent" })`.
- `auth: "trusted_backend"` is removed; the value is `"backend"`.
- `providers.guest({ actorPrefix })` is now `userPrefix` only.
- `github.credentials(...)`: the `"actor"` token source is removed in favor of
  `"user"`, and `resolveActorToken` / `resolve_actor_token` is now
  `resolveUserToken` / `resolve_user_token` only.
- Claim mappings take `user`, `groups`, and optional `email`; actor, tenant, and
  organization identity claims are removed.

**Resolved config — `IdentityConfig`** (`npm`, `pypi`)

The resolved contract now uses the same words as the authoring surface, so a
value read while debugging is the value that was written.

- `scoping` becomes `scope`; tenancy and organization requirements are removed.
- Axis values use `user`, `agent`, `none`, and `custom`; thread ownership is
  always user-scoped.
- `ScopingConfig` becomes `ScopeConfig`.
- Context Hub user memory uses `{deploy}--u--{user}`. The CLI still recognizes
  legacy `--t--` child repos during deletion so old resources can be cleaned up.

**Runtime envelope — `runtime.identity`** (`npm`, `pypi`)

- `identity.actor` becomes `identity.user`; tenant and organization fields are
  removed. The aliases are gone, so `runtime.identity?.actor.id` must become
  `runtime.identity?.user.id`.
- `user.type: "user" | "service"` becomes
  `user.kind: "person" | "service"`.
- New `identity.groups` carries every group the caller's token asserts for
  authorization decisions in tools and middleware; isolation keys on the user.

**Transport** (`npm`, `pypi`, `cli`)

- The trusted ingress header is `x-mda-user-id`; tenant, organization, and group
  identity headers are not accepted. Group memberships come only from validated
  token claims.
- `langgraph_auth_user` uses `mda_user_id`, `mda_user_email`, `mda_user_kind`, and
  `mda_groups`. Tenant and organization fields are removed, while reserved-key
  filtering still prevents request bodies from spoofing retired fields.
- Hosted credential token-exchange assertions carry `user_id` and `user_kind`;
  tenant and organization identity fields are removed.

**Plugin contracts** (`npm`, `pypi`)

- `IdentityConnectProvider`: `status`, `startAuthorize`, and `unlink` take
  `userId`; the `shouldMount` context field `scoping` is now `scope`.
- Slack identity links: record field `actorId` → `userId`, `slackActorId` →
  `slackKey`; `getByActorId` → `getByUserId`, `getBySlackActorId` →
  `getBySlackKey`, `removeByActorId` → `removeByUserId`.
- Slack channel filters: `includeActors` / `excludeActors` → `includeUsers` /
  `excludeUsers`; filter reasons `actor_filtered` → `user_filtered` and
  `ambiguous_actor_namespace` → `ambiguous_user_namespace`.

**CLI** (`cli`)

- `mda init --identity <preset>` is removed. Use
  `mda init --scope <user|agent|none>`; the retired preset names are no longer
  accepted as aliases.
- Eval `identity.json` fixtures use `user` and optional `groups`.

Unaffected on purpose: `LANGSMITH_TENANT_ID` and the CLI's `X-Tenant-Id` header
refer to the LangSmith workspace, not identity, and keep their names.

### Removed

#### BREAKING (validated-token provider helpers)

- `auth.auth0`, `auth.clerk`, `auth.okta`, `auth.cognito`, `auth.entra`,
  `auth.google`, `auth.oidc`, and `auth.langsmith` are removed from the public
  authoring surface. Use `auth.supabase` for validated-token ingress (`npm`,
  `pypi`).

#### BREAKING (guest ingress)

- Anonymous/guest ingress is removed in full (`npm`, `pypi`, `cli`). Gone: the
  `auth.guest(...)` authoring helper, `ValidatedTokenProvider.guest`, the
  `POST /identity/guest` issuance route and its legacy Chat LangChain
  `POST /api/auth/guest` counterpart, HS256 guest-token minting and
  verification, and `validateIdentity`'s `guest` verifier branch. Callers must
  authenticate with `auth.supabase` or use trusted-backend ingress.
- `MDA_GUEST_SIGNING_KEY` is **not** removed. Despite the name it is also the
  signing key for Connect-with-X OAuth `state` JWTs, so deployments using
  Connect must keep setting it. Only its guest-token usage is gone.
- `issueGuestToken` (npm `managed-deepagents/runtime`) and `issue_guest_token` /
  `issue_legacy_guest_token` / `verify_legacy_guest_token` (pypi
  `managed_deepagents.runtime`) are removed. The Python-only
  `_legacy_chat_langchain` module is deleted — it existed solely for guest.
- Internal rename: the auth-middleware bypass principal for public routes is now
  `mda:public-route` (was `mda:guest-issuer`), exposed as `publicRouteBypassUser`
  / `public_route_bypass_user`. It is a per-request synthetic identity, never
  persisted.

#### BREAKING (`auth.github`)

- The `auth.github()` validated-token provider is removed. It verified opaque
  GitHub OAuth access tokens by calling `GET https://api.github.com/user` on
  every request. Declare the same shape inline on `defineIdentity({ auth: ... })`
  if you need it — the `introspect` mechanism itself is unchanged (`npm`,
  `pypi`).
- `credentials.github(...)`, `connect.github()`, and the Connect-with-GitHub
  routes are unaffected; they are separate features that only share the name.

#### BREAKING (identity `scope`, `credentials`, `connect`)

- `defineIdentity` / `define_identity` no longer accept `scope`, `credentials`,
  or `connect`. Identity is managed: threads and downstream credentials are
  always per-caller. `auth` is the only remaining option, and `scope` fails with
  a message pointing at `memory.{ts,py}` for the axis that moved there
  (`npm`, `pypi`).
- This changes the resolved contract for existing projects that declared
  nothing: `defineIdentity()` used to resolve to `{credentials: "agent"}` and now
  resolves to `{credentials: "user"}`. Downstream calls carry the caller's own
  tokens through per-caller Connect rather than the shared LangSmith vault from
  `mda connect`. A deployment that relied on the shared vault has to move those
  integrations to per-caller Connect.
- Durable memory is unaffected: it is declared in `memory.{ts,py}` and was never
  part of this change.
- `mda init --scope <user|agent|none>` is replaced by the `mda init --identity`
  flag, which scaffolds the argument-free declaration (`cli`).
- Connect-with-GitHub no longer mounts from a `credentials.github(...)` chain,
  since that chain can no longer be declared. It mounts only for a user-scoped
  deployment that declares a GitHub connector (`npm`, `pypi`).

#### BREAKING (`connectors.github`)

- The `connectors.github` first-class connector is removed (sandbox repo
  checkouts, `gh` CLI install, GitHub App webhook Events ingress, and
  `POST /connectors/github/events`). Use custom tools or MCP for GitHub API
  access. Fleet/CLI `github-oauth-provider` is unchanged (`npm`, `pypi`).

#### BREAKING (`connectors.langsmith`)

- The `connectors.langsmith` capability-delegation connector is removed
  (authoring builders, HTTP routes under `/connectors/langsmith/capabilities/…`,
  and `CredentialTarget.kind: "langsmith"`). Custom LangSmith capability routes
  are out of scope while connector boundaries settle (`npm`, `pypi`).
  Sandbox backend behavior is unchanged, but declarations now use
  `defineSandbox(…)` / `define_sandbox(…)` instead of `sandboxes.langsmith(…)`.
  Definitions are data-only: provider classes and provider-generic sandbox
  types are internal, while TypeScript authors use the backend-neutral
  `SandboxOptions` type.

### Fixed

- A syntax error in an authored file is now reported as
  `failed to parse <file>:<line>:<column>: <message>` instead of being read as
  configuration that was never written. `mda build` used to discard parser
  diagnostics, so a stray brace in `agent.ts` produced "agent `name` is
  required" for a file whose name was right there, and a broken
  `channels/*.ts`, `connectors/*`, or `identity.*` was silently dropped from the
  deployment or deployed without its ingress secret. Applies to both languages;
  the Python extractors no longer swallow `SyntaxError`, and a missing `python3`
  is now distinguishable from "not configured" (`cli`)
- `mda build --out <dir>` no longer deletes a directory it does not own. The
  target must be missing, empty, or a directory a previous build wrote, and it
  can no longer be the project directory or an ancestor of it — `--out .` used
  to recursively empty the project, `.env` included (`cli`)
- Harbor evals: invoke Python trials asynchronously so async-only tools (MCP
  connectors) no longer fail the first tool call, matching the Node runner
- Harbor evals: forward every shell-exportable project `.env` key to the trial
  container so connector headers, MCP tokens, and tool API keys reach the agent
- Keep handoff credentials on loopback
- Generate internal handoff credentials
- Avoid remote verification for server handoffs
- Allow dynamic identity auth options
- Reject null LangSmith auth responses
- Recognize deploy-owned Context Hub repos in the collision gate (`deploy`)
- Limit channel event request bodies
- Drop removed defineIdentity options from fixtures (`integration-tests`)
- Allow empty params for slack (`npm`)
- Drop `scope` from the defineIdentity error text (`identity`)
- Repair scope-removal fallout (`identity`)
- Stop fixture and example prompts promising a user slice (`memory`)
- Migrate channel fixtures off the identity memory axis (`memory`)
- Refuse a scope a spread could decide (`memory`)
- Resolve conflict markers committed into .gitignore
- Match toolserver slugs case-insensitively in `--list` (`cli`)
- Drop void operator that fails oxlint no-void (`npm`)
- Repair clippy, oxfmt, and authoring export checks after rebase (`ci`)
- Discover OAuth provider slugs and scopes per install (`cli`)
- Strip tsx/cts from channel and connector stems (`runtime`)
- Discover OAuth provider slugs from toolserver catalog (`cli`) (#217)
- Persist LangSmith key and infer local public API URL for mda dev (`cli`) (#211)
- Keep execute mounted under user/org memory remounts (`runtime`) (#199)
- Mint LANGSMITH_API_KEY after device login for connect and dev (`cli`)
- Allow empty Enter for LangSmith browser sign-in (`cli`)
- Resolve npm/python on Windows and drop TS file: runtime dep (`cli`) (#178)
- Surface parse errors instead of deploying misread config (`cli`) (#167)
- Bound every outbound HTTP call in the TypeScript runtime (#166)
- Keep server-local requests and the ingress secret on-host (`runtime`) (#164)
- Stop mda build --out from deleting directories it does not own (`cli`) (#165)
- Clear a prior actor's token on sandbox reuse (`github connector`) (#163)
- Stop publishing a corrupted changelog and stale wheels, and gate release automation in CI (`release`) (#162)
- Invoke Python trials async and forward project env (`eval`) (#148)

## 0.4.2 - 2026-07-24

### Fixed

- Harbor evals: always template the model provider API key, honor project `.env`
- Harbor evals: write file tools to real disk under `/app` instead of StateBackend
- Ignore OS junk that breaks UTF-8 Context Hub sync (`cli`) (#146)
- Forward Harbor credentials and write trial files to disk (`eval`) (#143)
- Skip co-located tests and non-exports at startup (`connectors`) (#144)
- Use dotenvy for env file read (`cli`)
- Remove allowlist parameter from github connector (`runtime`) (#141)
ze
  `/app/...` paths so virtualMode does not double the root (`runtime`)
- Harbor evals: print the jobs directory and note that re-running the same
  command resumes cached trials (`cli`)
- Skip `connectors/` and `channels/` unit-test filenames and modules without the
  required plugin export so co-located tests and helpers are not imported at
  startup (`cli`, `npm`, `pypi`)

## 0.4.1 - 2026-07-22

### Fixed

- Forward LANGSMITH_API_KEY_GATEWAY to harbor output (`cli`)
## 0.4.0 - 2026-07-22

### Added

- Connector `sandbox` hook and per-connector plugin directories (`mcp`,
- Neutral channel manifest envelope + `ChannelProviderAdapter` registry; Slack
- `defineGitHubChannel` / `define_github_channel` — GitHub App webhook channel
- Channel **plugin** contract (`defineChannel` / `define_channel`, brand,
- Reference docs under `docs/` for building channel/connector plugins; product
- Plugin connectors/channels and GitHub App channel (`channels`) (#131)
- Add connector credentials, sandbox provisioning, and Connect-with-GitHub (`github`) (#93)
- Reuse LangChain and deepagents types in authoring APIs (`pypi`) (#123)
- Add Slack Events ingress with identity-scoped auto-reply (`channels`) (#101)
- Local Context Hub mock and identity-scoped remounts (`memory`) (#114)
- Add support for running evals with MDA (`cli`) (#100)

### Changed

- Clean up dead code (#139)
- Bump the npm_and_yarn group across 2 directories with 1 update (`deps`) (#138)
- Collapse duplicated helpers across CLI and runtimes (#128)
- Bump actions/setup-node in the major group (`deps`) (#117)
- Bump the minor-and-patch group with 3 updates (`deps`) (#118)
- Bump oxc from 0.139.0 to 0.140.0 in the major group (`deps`) (#119)
- Bump the minor-and-patch group (`deps-dev`) (#121)
- Bump typescript in /packages/npm in the major group (`deps-dev`) (#122)
- Export typed ManagedDeepAgentRuntime for tools and middleware (`pypi`) (#113)
- Fix release script CodeQL alerts (#107)
- Harden Rust CLI toward idiomatic patterns (`cli`) (#108)

### Fixed

- Require static name for deploy and assistant id (`cli`) (#137)
- Fail build on missing connector/channel exports (`compile`) (#134)
- Make Slack sandbox git/gh auth reliable end-to-end (`runtime`) (#132)
- Forward LLM gateway base URLs in Harbor jobs (`eval`) (#133)
- Run ci without omitting peer deps (`release`)
- Skip connect prompts on unlinked thread replies (`runtime`) (#124)
- Make github/slack/supabase UIs work on mobile (`examples`) (#125)
- Update format (`test`)
- Refresh stale seeds that teach /memories/AGENTS.md (`memory`)
- Guide version mismatch toward project-local mda (`cli`)
- Tighten Python runtime typing away from Any (`pypi`) (#112)
- Harden release helper file handling
- Patch Python dependency security alerts
- Retry project deletes on LangSmith 429s (`integ`) (#98)
- Cold vs hot memory (`runtime`) (#97)
- Clean up context hub entries (`test`) (#96)
- Require sandbox declaration and scaffold it in init (`cli`) (#95)
- Require MDA_INGRESS_SECRET for trusted_backend identity (`deploy`) (#94)
## 0.3.1 - 2026-07-13

### Changed

- Bump the minor-and-patch group across 1 directory with 2 updates (`deps-dev`) (#87)
- Update setuptools requirement in /packages/pypi (`deps-dev`) (#58)
- Bump cliclack in the minor-and-patch group (`deps`) (#85)
- Bump oxc from 0.138.0 to 0.139.0 in the major group (`deps`) (#86)

### Fixed

- Lock language and runtime to install channel (`cli`) (#92)
- Fix lock file (`npm`)
- Refresh npm lockfile on release finalize (`ci`)
- Update package-lock (`npm`)
- Create git tag before GitHub Release in finalize (`ci`)
## 0.3.0 - 2026-07-12

### Added

- Richer version output and help UX polish (`cli`)
- Managed identity, connectors, and Chat LangChain migration support (`identity`) (#83)
- Restore --deployment-type flag for managed deep agents (`cli`) (#78)

### Fixed

- Open studio from mda dev by default (#72)
## 0.2.0 - 2026-07-07

Published as `managed-deepagents==0.2.0` on PyPI. npm published the same CLI
release train as `managed-deepagents@0.1.0` (manifests were not yet aligned).
From the next release onward both packages share one version.

### Changed

- Reoriented the project from language-specific API SDKs to a single `mda` CLI,
  written in Rust and cross-compiled for distribution to npm and PyPI
  (`cli`, `npm`, `pypi`).
- Removed the previous Python (`python/`) and TypeScript (`js/`) SDKs.
- `mda build` and `mda deploy` take the project path as a positional argument
  (defaults to `.`) instead of `--root` (`cli`).

### Added

- `defineDeepAgent` / `define_deep_agent`: the v0 authoring contract. It accepts
  the full `createDeepAgent` surface minus the managed keys (`backend`, `store`,
  `checkpointer`) and returns a pre-runtime spec. Shipped from the TypeScript
  (`packages/npm`) and Python (`packages/pypi`) `managed-deepagents` packages,
  alongside a `runtime` helper (`compileManagedAgent` / `compile_managed_agent`)
  used by generated entry modules (`npm`, `pypi`).
- `mda build <project>` / `mda deploy <project>`: compiles a code-first Deep Agent
  project into a deployable managed LangGraph app. It copies your files
  verbatim, generates a managed entry module that consumes the `defineDeepAgent`
  definition and plugs it into an `agent(...)` graph factory, and generates
  `langgraph.json` (`cli`).
- Managed Context Hub memory backends, MCP connectors, schedules, and scoped
  LangSmith sandbox backends (`cli`, `npm`, `pypi`).
- Example TypeScript and Python Deep Agent projects under `examples/`.
- npm and PyPI packages that ship the authoring interface plus the prebuilt CLI
  binary (`npm`, `pypi`).

### Removed

- The AST transform of `agent.{ts,py}` (and the `oxc` / `rustpython-parser`
  dependencies). The CLI no longer rewrites user code; managed wiring lives in
  the generated entry module and the `defineDeepAgent` contract instead (`cli`).

## 0.1.0 - 2026-07-07

npm-only publish of the CLI-oriented `managed-deepagents` package
(`managed-deepagents@0.1.0`). See [0.2.0](#020---2026-07-07) for the shared
release notes for this train.

## 0.1.2 / 0.1.1

Earlier PyPI CLI packaging releases while npm was still on the `0.0.x` line.

## 0.0.2

Early npm packaging release of the CLI-oriented package
(`managed-deepagents@0.0.2`), with matching platform optional dependencies.

## 0.1.0 (API SDK)

Initial public beta SDK release (Python + TypeScript API clients). Superseded by
the CLI direction above.
