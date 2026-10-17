# TAC Project Ledger

Maintained per [Development_Protocol.txt](Development_Protocol.txt) Section 11. This ledger tracks the project's *current state*. Read it first to orient; consult [decision_log.md](decision_log.md) for rationale, history and active overrides only as needed. Do not rebuild the current state by reading the whole decision log.

When new evidence resolves an open question, update the ledger before building on that conclusion. Update entries in place so the ledger describes the present, but keep every correction visible (a struck-through line with a note, or "resolved, see below"); never rewrite silently. If a correction is material, add a decision log entry for it. Do not record the hash of HEAD here: it is always one commit stale.

## Up next

Cold start (replace this block as the state changes; read it first):

- Current fork follow-up (2026-10-17, DL-005; initial investigation/in-progress status resolved): complete own long-buff/song observations are now implemented in Box Network 1.2.0's existing heartbeat. Fresh usable reports drive ordered missing-buff rules and release obsolete inspection, preserving DL-004 freshness/identity, unknown/non-peer fallback, emergency healing and cast targeting/restoration. Focused local regressions pass 32,721 assertions with zero failures; five deliberate in-memory defects are caught, Lua 5.1/LuaJIT compilation passes, and the core remains at 181 slots. Deployment guidance is in README: update core and plugin on every participating character, enable Box Network and restart TAC. Normal publication to the same open PR is authorized; there is no live-game verification, game installation or separate PR comment. Necessary targeting to cast remains intentional.
- Current fork PR follow-up (2026-10-17, DL-004): Box Network cure reporting is implemented and locally validated on the existing cure PR branch, preserving its incoming merged `dev` work. Corrects failed reads becoming clean zeros, missing own affliction flags, and general messages refreshing old heartbeats. Both ordered selectors, fallback, emergency healing and target holding/restoration are covered by the focused real-path suites: 13,205 assertions pass, none fail; Lua 5.1 / LuaJIT compilation passes, core main chunk 181 slots. Normal publication is authorized; no live installation or PR comment is authorized. Matching core/plugin deployment and server-side cure success remain unverified. Update core and Box Network on participating characters and restart TAC; `/ac net debug` now shows report version/schema, heartbeat age and usability.
- The development protocol was adopted on 2026-10-13. This ledger, the decision log and the lessons log were created that day. The decision log holds one retrofit entry, DL-001, covering the agreements of that day; the ledger and lessons log hold no further entries.
- Done and merged into local `dev` (not pushed): TAC's logs move to `Logs\TAC\` (DL-002). The developer called the live check done on 2026-10-13 after the main log, `/ac dump` files and chat tab logs were seen landing in `Logs\TAC\`. **Still installed in MacroQuest: test build `v3.2.0-log-folder-1`**, that is the merged `dev` files with `VERSION` stamped in the installed `triune.lua` only; what to do with it is not decided. The files it replaced are backed up in `C:\Users\legal\TAC-backup-20261013-140007\` (the earlier `TAC-backup-20261013-075343` also remains).
- Done and merged into local `dev` (not pushed): priority ordering for `onCommand` and `onBetweenPulls` (DL-003). All four design decisions were reviewed by ChatGPT and approved by the developer; the implementation was reviewed by ChatGPT (snapshot `70245f7`, recommended for merge) and the developer said "Merge it." Built and passing local tests and a 15-point mutation check. **Not installed in MacroQuest, nothing verified live; the developer skipped the live check.** Shipped-command check (static, 2026-10-13, corrected scan): the 18 plugins that implement `onCommand` compare `cmd` with 98 distinct command names and **no two plugin files share one**, so the new id order should not change which plugin answers any shipped command. This is a text scan of each `onCommand` body, not a run in the game; it does not see commands handled some other way, and it does not cover the core's own `/ac` commands (those are handled before plugins are asked). Before a release: run `luacheck` and `luac5.1` (CI), neither of which has run on this change.
- Installed in MacroQuest (2026-10-13, at the developer's request): clean `dev` at the merge of DL-003, `VERSION` `3.2`, no test stamp. It replaced test build `v3.2.0-log-folder-1`; the only file that differed was `lua/triune.lua`, and every `lua/` and `config/` file now matches `dev` (compared with line endings ignored). The replaced file is in `C:\Users\legal\TAC-backup-20261013-171237\`; the earlier backups `...-075343` and `...-140007` also remain until something is approved for `main`. The placeholder `TAC/Logs/TAC/README.txt` was not installed (the folder already exists). **TAC needs a restart to load it.** The hook-priority code is now installed but has not been run in the game.

## Pending live verification

Implemented but not yet confirmed in the live game.

- Box Network cure reporting (DL-004): reproduce the reported curse after updating `triune.lua` and `tac/boxnet.lua` and restarting TAC on support and recipient. The local environment cannot establish the user's active plugin versions, actual affliction readings or the item's server-side result.
- Box Network buff observations (DL-005): after updating both files on participating characters, observe whether usable fresh reports eliminate inspection-only groupmate cycling under the user's actual rules. `/ac net debug` identifies report completeness, age and usability; unknown/older peers still use fallback, and actual casts still target recipients. The local environment cannot verify native client readings or server-side buff/cure results.
- `Logs\TAC\` (DL-002), the parts never observed live: the chat draw trace and chat capture files (local tests only); that creating the folder does not stall the client (not measured); rotation of the main log to `.old` inside `Logs\TAC\`; that a release zip extracts the shipped `TAC/Logs/TAC/README.txt` into `Logs\TAC\`. The developer accepted the live check as done without these.

## Resolved behavior

Only behavior we have actually agreed upon.

- TAC's logs go to `Logs\TAC\` (requirements in DL-002; built, merged into local `dev`, live-checked for the main log, dump files and chat tab logs). Chat history stays in `config`; old log files stay where they are.
- Test builds are named `v3.2.0-<feature>-<N>`: the base version, the feature, then a counter that rises with each build of that feature (developer, 2026-10-13).
- The existing fork PR's cure follow-up uses fresh own-character Box Network affliction reports without discovery targeting, while preserving fallback for unknown/stale/older peers, ordered selection and heal/cast safeguards (contributor request, 2026-10-17; DL-004).
- The same fork PR uses fresh complete Box Network long-buff/song reports for ordered missing-buff rules, preserving recipient-specific matching/refresh behavior and unknown/stale/older-peer fallback rather than claiming missing data means missing buffs (contributor request, 2026-10-17; DL-005).

## Confirmed live/system facts

Facts established through testing, source inspection, logs, or documentation.

- MacroQuest's docs say the logs folder is configurable and must be read from `${MacroQuest.Path[logs]}` (`reference/data-types/datatype-macroquest.md`, docs commit `a85c4a6`, read 2026-10-13).
- `lfs` is not bundled with MacroQuest; its docs describe it as a LuaRocks module installed through PackageMan (`lua/luarocks-modules.md`). LuaFileSystem 1.9.0 is installed on the developer's machine and its manual documents `lfs.mkdir` (read 2026-10-13).
- Before DL-002, TAC wrote the main log to `config/../Logs` (a guess) and the chat logs to `MacroQuest.Path('logs')`, and nothing in TAC created folders (code reading, 2026-10-13).
- Live, 2026-10-13, test build `v3.2.0-log-folder-1` (read from disk): TAC created `Logs\TAC\` itself with `lfs.mkdir` using the mixed-separator path `C:\Users\Public\MacroQuest\Logs/TAC`; the main log, a `/ac dump` file and a chat tab log (`tac_chat_Kylaeris_All_20261013.txt`) were written there, and no chat file was written anywhere else (DL-002 addenda).
- Source inspection, 2026-10-17: MacroQuest's own affliction flags inspect buff SPAs, while aggregate `Counters*` read client affect-slot values (`MQ2CharacterType.cpp` / `MQ2Spells.cpp`). Box Network already transports counters; no new channel is required (DL-004).
- Source inspection, 2026-10-17: `Me.Buff` / `Me.Song` are slot-indexed, native long-buff/song counts are separate, and `Buff.Duration` supplies remaining time. The shipped Effects window scans full slot arrays rather than assuming counts are compact slot bounds (DL-005).

## Open implementation details

Questions intentionally unresolved; surface them for discussion when they become relevant.

- How the Protocol's file schema (logs in `macroquest\logs\<luaname>\`, config in `macroquest\config\<luaname>\`) applies to existing TAC files: the developer has said logs move out of `config` first; what happens to the per-server loadout, chat and DPS files, and the exact folder names, are not decided.
- How pre-release test build names fit with the version-must-match check between `triune.lua` and `README.md`. For `v3.2.0-log-folder-1` the name was stamped into the installed `triune.lua` only and not committed; whether that is the standing method is not decided.

## Out of scope

Things we have explicitly decided not to build or investigate. Nothing yet.
