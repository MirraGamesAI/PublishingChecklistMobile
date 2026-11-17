### About PublishingChecklistMobile

One checklist for publishing Unity games on 9 mobile stores, kept by Mirra Games. It covers the game builds, not the store pages.

It merges the rules of Google Play, the Apple App Store and 7 other Android stores into one set. Main items pass in every store build, and items tagged with a store name apply only to that store's build. Pass both, and each build is ready for its store.

### Features

1. One checklist for 9 mobile stores.
2. 257 checks, 88 ready for automation.
3. English and Russian, item for item.
4. A source for every store rule.
5. Print-ready PDFs from one command.

### Requirements

1. Node.js 18 or newer and Chrome or Edge 131 or newer, to build the PDFs.
2. Unity 6000.0.68f1 or newer, or 6000.3.8f1 or newer, for the games it checks.

### Limitations

1. Epic Games Store and mainland China stores are not covered.
2. Store page material and games made for children are not covered.

### How to use

| Path | Purpose |
| --- | --- |
| [Markdown/publishing-checklist.md](Markdown/publishing-checklist.md) | The checklist in English |
| [Markdown/publishing-checklist-russian.md](Markdown/publishing-checklist-russian.md) | The same checklist in Russian |
| [Tools/PrintPDF](Tools/PrintPDF/README.md) | Builds print-ready PDFs of both |
| [Documentation/Research](Documentation/Research/conflicts.md) | Store research and the rule-to-check matrix |
| [CHANGELOG.md](CHANGELOG.md) | What changed in each version |

Build the PDFs. They appear in `Tools/PrintPDF/Output/`:

```bash
node Tools/PrintPDF/build.mjs
```

To edit the checklist:

1. Change both language files together, so they stay the same item for item.
2. Keep item numbers permanent: a new item takes the next free number in its section, and a removed number is never reused.
3. Put the checks a person must do first. Checks a script or an AI can take over go under "Can be automated" with an `Auto test` or `Ask AI` marker.
4. Raise the version in `CHANGELOG.md`. The PDF cover reads it from there.
