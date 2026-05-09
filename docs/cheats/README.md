# Bundled Cheats

The PNACH files bundled in `app/src/main/assets/cheats` were imported from
`https://github.com/noeldvictor/NetherSX2-patch`, `cheats/exact`.

That source repo is released under the Unlicense. ARMSX2 keeps only the exact
CRC cheat pack by default. Candidate PNACH files are intentionally excluded
because the source marks them as requiring in-game testing.

The source cheat pack stores gameplay cheat lines as commented `// patch=...`
entries for NetherSX2's file-edit toggle flow. ARMSX2 imports them as normal
`patch=...` entries inside named PNACH sections so the in-game per-section
switches control activation through PCSX2's cheat enable list.
