# Personal MMU fork

Personal fork: <https://github.com/tchejunior/Prusa-Firmware-MMU>

Branch: `codex/personal-mmu`, based on upstream `v3.0.4` (`48d4d92`).
This branch currently adds maintenance documentation only; MMU firmware source
is unchanged. The current paired Buddy v6.5.7 branch is
<https://github.com/tchejunior/Prusa-Firmware-Buddy/tree/codex/personal-coreone-6.5.7>.
The earlier Buddy 6.8.1 and 6.10.1 branches remain available for reference.

FINDA warning followed by ADC-triggered replacement loading, and the separate
internal-filtration mode, are implemented on Buddy. Recovery uses existing MMU
3.0.4 registers to verify the selector slot and synchronize remembered filament
state. No new MMU firmware build or flash is required for these changes.

This standalone repository is the MMU firmware source of truth. Do not use the
embedded `lib/Prusa-Firmware-MMU` copy in Buddy for MMU development or builds.

## Staying current without publishing to upstream

The local clone has `origin` pointing to the personal fork and `upstream` pointing
to `prusa3d/Prusa-Firmware-MMU`. The upstream push URL is `DISABLED`.
`remote.pushDefault=origin`, `push.default=current`, and `rerere.enabled=true`
are configured locally. No upstream pull requests are needed.

```powershell
git fetch upstream --tags
# Replace NEW_TAG with the chosen Buddy-compatible MMU release tag.
git switch -c codex/mmu-NEW_TAG NEW_TAG
# Cherry-pick the personal documentation and any later firmware patches.
git log --oneline v3.0.4..codex/personal-mmu
git cherry-pick PERSONAL_COMMIT
git push -u origin HEAD
```

Retain the old tested branch when porting. Validate Buddy/MMU compatibility,
review conflicts and build/test actual MMU source changes before flashing.
Fetching upstream alone does not alter the personal branch or installed firmware.
