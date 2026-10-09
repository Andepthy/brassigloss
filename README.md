<div align="center">
<img src="https://raw.githubusercontent.com/Andepthy/brassigloss/main/public/favicon.svg" width="128" alt="Brassigloss icon">

---

# Brassigloss

![GitHub License](https://img.shields.io/github/license/Andepthy/brassigloss)
[![GitHub stars](https://img.shields.io/github/stars/Andepthy/brassigloss)](https://github.com/Andepthy/brassigloss/stargazers)
[![GitHub issues](https://img.shields.io/github/issues/Andepthy/brassigloss)](https://github.com/Andepthy/brassigloss/issues)
</div>

Brassigloss is a Vue 3 single-page application for browsing, searching, and comparing translation text for games and mods.

The project currently includes translation files for Create, Create Aeronautics, and Chants of Sennaar. You can filter by project and language, and view source text and translations side by side in a table.

> The Apache-2.0 license for this project applies only to the software code written by this project. Names, source text, translations, and other third-party content provided by games, mods, publishers, and their localization contributors are not covered by that license. See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) for details.

## Origin and AI Disclosure

- This project is heavily inspired by [Verdigloss](https://github.com/SkyEye-FAST/verdigloss) and has been adapted on top of it for the current translation data. This project is not an official fork, successor, or endorsed version of Verdigloss.
- AI coding tools were used during development to assist with writing, refactoring, and organizing code, documentation, and test-related content. Content generated or modified by AI is reviewed, adjusted, and owned by the project maintainers.

## Demo

Brassigloss is published via GitHub Pages:

- <https://andepthy.github.io/brassigloss/>

## Features

- [x] Search by translation key or by text in any selected language
- [x] Multi-select filtering by project, language, and text category
- [x] Dynamically show available language columns based on the selected project
- [x] Paginated browsing of large numbers of translation entries
- [x] Dark and light theme switching
- [x] Serif and sans-serif font switching
- [x] Responsive translation comparison table

## Architecture

- `src/app/` configures application startup and mounting.
- `src/components/` contains the app header, query controls, pagination, and the translation comparison table.
- `src/composables/` manages theme, font, and compact layout preferences.
- `src/features/` contains business logic such as filtering, project cataloging, and pagination.
- `src/services/` loads runtime translation data.
- `scripts/preprocess.mjs` discovers data sources and generates the unified JSON used by the app.
- `scripts/lib/` provides preprocessing modules such as CSV parsing and data source discovery.
- `scripts/windows/` provides convenience launch and data update scripts for Windows.

The main directory structure is as follows:

```text
.
|-- data/
|   |-- aeronautics/                    # Create Aeronautics translation data
|   |-- chants-of-sennaar/              # Chants of Sennaar CSV data
|   `-- create/                         # Create translation data
|-- public/data/translations.json       # Generated file read by the app at runtime
|-- scripts/                            # Data preprocessing and convenience scripts
|-- src/                                # Vue application source
|-- index.html
|-- package.json
|-- pnpm-lock.yaml
|-- vite.config.js
|-- LICENSE
|-- README.md
`-- THIRD_PARTY_NOTICES.md
```

## Development

Brassigloss requires Node.js ^20.19.0 or >=22.12.0 and uses pnpm to manage dependencies.

1. Install dependencies:

   ```shell
   pnpm install
   ```

2. Generate the translation data used by the app from `data/`:

   ```shell
   pnpm preprocess
   ```

3. Start the development server:

   ```shell
   pnpm dev
   ```

4. Open <http://localhost:5173/> in your browser.

Common commands:

```shell
pnpm dev          # Start the Vite development server
pnpm preprocess   # Regenerate public/data/translations.json
pnpm test         # Run data processing and frontend logic tests
pnpm build        # Create a production build
pnpm preview      # Preview the production build locally
```

`pnpm preprocess` reads the JSON and CSV files under `data/` and overwrites `public/data/translations.json`. Run this command first on a fresh checkout or after updating data.

## Translation Data

The preprocessing script treats each direct subdirectory under `data/` as a data source and uses the folder name directly as the display name in the "project filter". The same mod can be split into multiple directories by namespace; these directories are displayed separately, but that does not mean they are independent mods.

- JSON projects: each `<language code>.json` file represents one language, such as `en_us.json`, `zh_cn.json`, or `lzh.json`. The script automatically merges language files and translation keys within the same project, so you do not need to register projects or languages in code.
- CSV projects: the file must contain a `key` column. Language columns may use compatible headers such as `English`, `French`, `SimplifiedChinese`, or `TraditionalChinese`, or they may use language codes in the `en_us` or `pt_br` form directly.

After adding folders or files under `data/` that follow the patterns above, just run `pnpm preprocess` and the app will automatically display the new projects and languages without any code changes.

All data is ultimately written to `public/data/translations.json`. This file is generated by the script and should not be modified by hand.

## Deployment

`.github/workflows/deploy-pages.yml` runs dependency installation, translation data generation, and the production build on pushes to `main` or on manual triggers, and publishes `dist/` to GitHub Pages.

## Third-Party Content

The following content belongs to the respective games, mods, publishers, developers, translators, or localization contributors and is not covered by the license for this project's code:

- `data/aeronautics/**`
- `data/chants-of-sennaar/**`
- `data/create/**`
- Other namespace data under `data/` related to the same mods as above
- Content generated from that data in `public/data/translations.json`

This repository includes these texts for translation study, comparison, and non-commercial reference purposes. The project maintainers do not claim ownership of third-party game names, source text, translations, trademarks, or other intellectual property. If a rights holder wishes to correct attribution or have content removed, please contact the maintainers through a repository issue.

This project is inspired by Verdigloss:

- Project: <https://github.com/SkyEye-FAST/verdigloss>
- Author: SkyEye_FAST
- License: Apache License 2.0

This project is not affiliated with, sponsored by, or officially endorsed by Mojang Studios, Microsoft, the Create Mod team, the authors of related add-on mods, or the rights holders of Chants of Sennaar. All product names and trademarks belong to their respective owners.

## License

Except for parts explicitly marked as third-party content, the code written by this project is licensed under the [Apache License 2.0](LICENSE).

```text
    Brassigloss
    Copyright (c) 2026 Brassigloss contributors

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0
```

Third-party software dependencies remain subject to their own licenses; the complete dependency record is in `pnpm-lock.yaml`. See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) for third-party notices.

## Feedback

If you run into problems or have feature suggestions, issues and pull requests are welcome.
