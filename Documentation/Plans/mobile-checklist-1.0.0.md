# Mobile Checklist 1.0.0

- **Status:** In progress (3/12 tasks complete | Next: B1)
- **Total Estimate:** 6h 30m active, plus about 45m of agent wall time overlapped by B2 and the user's review time in C2 (Remaining: 6h 05m)
- **Goal:** Publish the Unity Mobile Publishing Checklist 1.0.0 in `MirraGamesAI/PublishingChecklistMobile`: English and Russian files, identical item for item, whose main items plus store-tagged items make each per-store build (AAB or APK for 9 Android stores, IPA for Apple) pass review in all 10 covered stores. Done when every store rule found in research is either a checklist item or a recorded drop with a reason, and both PDFs build with zero warnings.

### Stack

- **Content:** Markdown, restricted to the subset parsed by `Tools/PrintPDF/build.mjs` and documented in `D:\github-mirragames-ai\PublishingChecklistWebGL\Tools\PrintPDF\README.md`.
- **PDF:** Node.js 24.22.1 (18 or newer required) and Chrome 131 or newer at `C:\Program Files\Google\Chrome\Application\chrome.exe`. Fonts load from Google Fonts, so the build needs network access.
- **Research:** 7 `general-purpose` agents with web search and fetch, running in parallel. They write Markdown into `Documentation/Research/`.
- **GitHub:** `gh` 2.103.2, authenticated with admin rights on both repositories. `MirraGamesAI/PublishingChecklistAndroid` is public and `MirraGamesAI/AgentSkillsAndroid` is private, and both had no commits on 2026-11-17.
- **Unity context (hints only):** the floor is 2022.3 LTS, as in `AgentSkillsWebGL`. The store layer is MirraSDK5 5.2.3 (`https://github.com/MirraSDK/SDK5`, local copy `D:\github-mirrasdk\SDK5`).

### Locked Decisions and Invariants

The user approved decisions 1-6 and 13 in chat on 2026-11-17. The others are defaults taken from the Web repository and change only with the user's approval.

1. **Naming:** `PublishingChecklistAndroid` is renamed to `PublishingChecklistMobile`, and `AgentSkillsAndroid` to `AgentSkillsMobile`. GitHub redirects the old URLs. The title is "Unity Mobile Publishing Checklist", version 1.0.0. Rejected: an Android-only list with a separate iOS list later (most items duplicated, the lists drift apart); keeping the Android name while covering iOS (misleading).
2. **Build model:** one codebase, one build per store. A store layer swaps payments, ads, login, rating prompts and cloud saves at build time, and each build links only its own store's SDKs. Rejected: one APK that detects the installing store at runtime (developers report Google Play rejecting builds that merely contain Huawei libraries, and a Google services dependency breaks Huawei and Fire devices); one bare APK without purchases or store services (loses purchases; possible later as an optional "ads only" mode).
3. **Stores:** the 10 stores in the tag table. Excluded:
   - every mainland China store, including MirraSDK5 `MiAppMall` (`app.mi.com`) and Xiaomi Game Center, because they need a government game license, a Chinese publisher, real-name checks and anti-addiction limits;
   - TapTap International, because whether it accepts new outside submissions was unconfirmed on 2026-11-17;
   - APK mirror sites;
   - Epic on iOS, which is an EU-only alternative marketplace.

   The Amazon Appstore has been limited to Fire devices since 2025-08-20 and is covered on Fire tablets only.
4. **Epic is a partial source.** If research finds no public developer rules, Epic leaves 1.0.0 and the CHANGELOG names it as planned. Epic never blocks the release.
5. **Scope:** everything needed to produce and verify a store build (AAB, APK, Xcode project and IPA): code, SDKs, settings, manifests, signing and packaging. A step outside the build becomes an item only if it changes the build or blocks installs:
   - Android developer verification: the package name and signing key registered with Google. It is enforced on certified devices from 2026-09-30 in Brazil, Indonesia, Singapore and Thailand, with more regions in 2027.
   - Device availability.
   - A hand-off list delivered with each build that names every SDK, permission and type of collected data, for store forms.

   Store page material and the store forms themselves are excluded.
6. **Audience:** games are not aimed at children. Every game is declared 13+ in all stores and stays out of Apple's Kids category, so the Google Play Families policy and Apple's Kids rules are out of scope. Content stays family-friendly as in Web M1, and one item checks that nothing in the game targets children. Rejected: an Optional "Made for children" block (heavy research, different ad SDKs); all-ages targeting (the strictest ad rules on every game).
7. **Rule merging:** a rule every store accepts becomes a main item in its strictest variant. A rule that cannot hold in every build becomes a store-tagged item, enabled in that store's build. Every conflict and its resolution is recorded in `Documentation/Research/conflicts.md`.
8. **Format:** identical to Web 2.0.0. It covers the parser subset of `build.mjs`, the cover warning and "How to read" list, `(Optional)` blocks (purchases, rewarded ads, login, social, multiplayer), `- Unity:` hint lines, a Sources section with "partial" marks and a "Checked on" line. Human checks come first in each section, followed by `**Can be automated**` items marked `Auto test` or `Ask AI`. Item numbers are permanent: a new item takes the next free number in its section, and a removed number is never reused. Reason for the identical format: PrintPDF and the `AgentSkillsWebGL` `Tools/SyncChecklist` parser are reused unchanged by a future `AgentSkillsMobile`.
9. **Sections:** A-M keep the Web topics, so QA maps Web and Mobile items by letter. N and O are mobile-only. See the section table.
10. **Tags:** an item without a tag applies to every build, Android and iOS. `Android` is a group tag for all 9 Android stores and is not listed as a platform on the cover. `Apple` marks iOS-only items.
11. **Languages:** English is the master. Russian is translated after the user approves the English draft, item for item, reusing the terms of the Web Russian file: `Для отдельных площадок`, `Можно автоматизировать`, `Опционально`, `Автотест`, `Спросить ИИ`, `Проверено`.
12. **Unity hints:** the floor is 2022.3 LTS. Technical research (B1 group 7) sets the minimum patch that meets target API 36, 16 KB pages and the current Xcode requirement. If 2022.3 cannot meet a store requirement, the floor becomes the lowest Unity 6 patch that does, and the item states the reason.

    Hints name MirraSDK5 as the Unity store layer, the way the Web list names MirraGamesTemplate. Its Android configurations are `GooglePlay`, `HuaweiAppGallery`, `SamsungGalaxyStore`, `XiaomiGames`, `RuStore`, `OneStore`, `AmazonAppStore` and `Aptoide`, and its iOS configuration is `AppleAppStore`. All of them still use `Fallback*` providers for ads, payments and player account. SDK5 changes are out of scope: the gaps are reported to the user at the end and are not written into the checklist.
13. **Research:** 7 agents in parallel, in the groups listed in B1. Official sources come first; a third-party source is used only when no official one exists, and is marked as third-party. Every rule row carries a source URL. The "Checked on" date is the date B3 finishes.
14. **Seed facts:** these come from chat-time searches. Verify them and never trust them as given.
    - Google Play: target API 36 for new apps and updates since 2026-08-31; 16 KB page support for apps targeting Android 15 and higher since 2025-11-01; AAB required for new apps; Play Billing Library 8 required for updates since 2026-08-31; privacy policy and account deletion available inside the app.
    - Apple: privacy policy reachable inside the app (5.1.1(i)); account deletion inside the app when accounts exist (5.1.1(v)); privacy manifests for listed SDKs; ATT before any tracking; Restore Purchases; no mentions of other platforms (2.3.10); only the system review prompt (5.6.1); a privacy-focused login option whenever third-party login exists (4.8).
    - Several stores: loot box odds disclosure (Apple, Google, and Korean law for ONE Store); a Google-certified consent tool for the EEA, UK and Switzerland.
    - Ad networks and Google services: AdMob availability in Russia; no Google services on Huawei and Fire devices.
    - ONE Store Global: 122 countries from one global build, with its own payments in 7 countries.
15. **Web rules that are reversed on mobile:**
    - Web M14 bans every outgoing link, but mobile builds need a privacy policy link.
    - Web F21 bans vibration, but mobile allows haptics with a toggle.
    - Web has no Back button to handle, but the Android Back button must work on every screen.
    - Web M24 bans store mentions, but each mobile build mentions only its own store.
    - Web G21 sets orientation in the platform console, but mobile sets it in Player Settings.

    Web items about WebGL templates, browsers, compression headers and the cursor are dropped.
16. **Files:** `Documentation/` (this plan and the research) is committed, as in `AgentSkillsWebGL`. The repository is public, so no file contains personal data such as emails or account names.
17. **Git:** the initial commit `create: base structure` is on `main`. All other work goes on `feature/checklist-1.0.0`, committed after each finished step. Commit messages are one lowercase line, `<subject>: <intent>`, at most 25 characters, with no body and no trailers, as in the sibling repositories (`create: root readme`, `polish: cover layout`). The work ends in one squash PR titled `feature: checklist 1.0.0`, whose description uses the CHANGELOG `### What's new` format. Every push, the PR creation and the merge each need the user's go-ahead in chat.
18. **Out of scope for 1.0.0:** `AgentSkillsMobile` content, SDK5 changes, store page material, children's rules, mainland China, and TV, watch, car, PC and Mac targets.

### Tags

| Tag | Store | Coverage | MirraSDK5 configuration |
| --- | --- | --- | --- |
| `Google Play` | Google Play | Worldwide | `GooglePlay` |
| `Apple` | Apple App Store | iPhone, iPad | `AppleAppStore` |
| `Huawei` | Huawei AppGallery | Outside mainland China | `HuaweiAppGallery` |
| `Samsung` | Samsung Galaxy Store | Worldwide | `SamsungGalaxyStore` |
| `Xiaomi` | Xiaomi GetApps | Outside mainland China | `XiaomiGames` |
| `RuStore` | RuStore | Russia | `RuStore` |
| `ONE Store` | ONE Store | Korea and ONE Store Global | `OneStore` |
| `Amazon` | Amazon Appstore | Fire tablets | `AmazonAppStore` |
| `Aptoide` | Aptoide | Worldwide | `Aptoide` |
| `Epic` | Epic Games Store | Android, partial | none |
| `Android` | Group tag for all 9 Android stores | Not shown on the cover | - |

### Sections

| Letter | Section | What it covers on mobile |
| --- | --- | --- |
| A | Build & performance | Download and install size per store, startup time, frame rate, memory, crashes and ANRs, device range, minimum OS version |
| B | Advertisement | The Web ad rules, each store build's own ad SDKs, consent before the first ad request |
| C | In-app purchases (Optional) | Store billing only, restore, pending purchases, loot box odds |
| D | User data | Saves, cloud saves, login (Optional), account deletion |
| E | Analytics & events | Third-party analytics only after consent, and the store's own events |
| F | Controls | Touch only, Android Back, system gestures |
| G | User interface | Safe areas and notches, aspect ratios, tablets, orientation in Player Settings |
| H | Localization | The Web rules plus any language a store requires |
| I | Audio | The iOS silent switch, Android audio focus, calls |
| J | Pause | App lifecycle: background, interruptions, notifications |
| K | Social interactions (Optional) | Rating prompts through store APIs, store game services, sharing |
| L | Multiplayer (Optional) | The Web rules |
| M | Content & links | Content, copyright, links (with the privacy policy exception), the 13+ audience |
| N | Store builds | Each store's SDKs isolated in its build, package name, signing, AAB or APK, target and minimum API, 64-bit, 16 KB pages, Xcode version, developer verification, device availability, hand-off list |
| O | Privacy & permissions | Permissions, ATT, consent, privacy manifest, `Info.plist` usage strings, privacy policy link, the export compliance key |

### Scoped File Map

- **Work scope:** repository root `D:\github-mirragames-ai\PublishingChecklistMobile`.
- **Created here:** `Markdown/publishing-checklist.md`, `Markdown/publishing-checklist-russian.md`, `Tools/PrintPDF/`, `Documentation/Research/*.md`, `README.md`, `CHANGELOG.md`, `.gitignore`.
- **Reference, read-only:** the Web repository `D:\github-mirragames-ai\PublishingChecklistWebGL`: `Markdown/publishing-checklist.md` and `-russian.md`, `Tools/PrintPDF/build.mjs` (`PLATFORMS`, `DEFAULT_DOCUMENTS`, `LANGUAGES`), `README.md`, `CHANGELOG.md`. Also SDK5 `Runtime/Android/Configurations/` and `Runtime/iOS/`.

### Priority Scopes

#### A. Repository base (Independent | Est: 20m)

- [x] **A1. Rename both GitHub repositories and update the remotes** (Independent | Est: 10m)
  - **Context:** Decision 1. Both repositories are empty, so no history moves.
  - **Scope & Entry:** GitHub `MirraGamesAI/PublishingChecklistAndroid` and `MirraGamesAI/AgentSkillsAndroid`; local clones `D:\github-mirragames-ai\PublishingChecklistAndroid` and `D:\github-mirragames-ai\AgentSkillsAndroid`.
  - **Action:**
    1. `gh repo rename PublishingChecklistMobile -R MirraGamesAI/PublishingChecklistAndroid --yes`
    2. `gh repo rename AgentSkillsMobile -R MirraGamesAI/AgentSkillsAndroid --yes`
    3. `git remote set-url origin https://github.com/MirraGamesAI/<new name>.git` in each clone.

    The local folders keep their old names until E2.
  - **Verify:** `gh repo view MirraGamesAI/PublishingChecklistMobile --json name` and `gh repo view MirraGamesAI/AgentSkillsMobile --json name` both succeed, and `git remote -v` in both clones shows the new URLs.
  - **Note:** Done on 2026-11-17. `PublishingChecklistMobile` is public and `AgentSkillsMobile` is private, and `git ls-remote origin` works with the new URL.

- [x] **A2. Create the base commit and the feature branch** (Depends on: A1 | Est: 10m)
  - **Context:** Decision 17. An empty repository needs a commit on `main` as the PR base.
  - **Scope & Entry:** repository root, `.gitignore` (new).
  - **Action:** Write `.gitignore` containing `.claude/`, as in Web. Commit it on `main` as `create: base structure`. Branch `feature/checklist-1.0.0` from that commit and commit this plan on it as `create: checklist plan`. Push nothing.
  - **Verify:** `git log --oneline main` shows exactly 1 commit, and `git branch --show-current` prints `feature/checklist-1.0.0`.
  - **Note:** Done on 2026-11-17, `main` at `fbe6dd7`.

#### B. Research and tooling (Depends on: A | Est: 2h)

- [ ] **B1. Launch 7 research agents in parallel** (Depends on: A2 | Est: 15m active, about 45m wall)
  - **Context:** Decisions 3-6, 13 and 14. Agents write to disk, so the research survives a context reset.
  - **Scope & Entry:** `Documentation/Research/` (new).
  - **Action:** Send one message with 7 background `general-purpose` Agent calls. Each agent writes only its own file:
    1. `google-play.md`: Google Play Developer Program Policies and Play Console requirements.
    2. `apple.md`: App Review Guidelines, privacy manifests, ATT, the minimum Xcode and SDK version, `Info.plist` keys, export compliance.
    3. `huawei-xiaomi.md`: Huawei AppGallery and Xiaomi GetApps, outside mainland China only.
    4. `samsung-amazon.md`: Samsung Galaxy Store, and the Amazon Appstore on Fire tablets.
    5. `rustore-onestore.md`: RuStore, including non-resident developers; ONE Store Korea and ONE Store Global.
    6. `aptoide-epic.md`: Aptoide, including AppCoins (Catappult) billing; Epic Games Store on Android (partial).
    7. `technical.md`: technical requirements shared across stores:
       - target and minimum API per store, 16 KB pages, 64-bit;
       - AAB or APK and the size limits per store, signing schemes, Android developer verification;
       - the iOS SDK and Xcode minimum, privacy manifests and required-reason APIs for Unity;
       - ad network availability without Google services and in Russia, consent through UMP;
       - Unity IAP store coverage, and the minimum Unity patch for each item.

    Each brief contains:
    - the store list and exclusions (decision 3), the scope (decision 5) and the audience (decision 6);
    - the section table A-O;
    - the group's seed facts from decision 14, labelled "verify, do not trust";
    - an instruction to skip rules about store page material and children's apps;
    - this output template:

    ```
    # <Group> requirements

    Checked on <YYYY-MM-DD>.

    ## Sources

    1. [<title>](<url>) - official | third-party, partial when the store publishes only part of its rules

    ## Rules

    | # | Store | Section | Rule, one checkable statement | Level | Source |

    ## Build facts

    Formats, size limits, minimum and target API, signing, required SDKs (billing, ads, login, saves, review prompt), forbidden SDKs, permissions and APIs.

    ## Conflicts and open questions
    ```

    Level is `must` when breaking the rule causes rejection or removal, and `should` for quality or featuring guidance.
  - **Verify:** see B3.

- [ ] **B2. Adapt PrintPDF for the mobile checklist** (Depends on: A2 | Est: 30m, done while the B1 agents run)
  - **Context:** Decisions 8 and 10. The tag table is the source for `PLATFORMS`.
  - **Scope & Entry:** `Tools/PrintPDF/` (new), `Entry: Tools/PrintPDF/build.mjs#PLATFORMS`.
  - **Action:**
    1. Copy `build.mjs`, `README.md`, `.gitignore` and `Assets/MirraGames.png` from Web `Tools/PrintPDF/`, without `Output/`.
    2. Replace `PLATFORMS` with the 11 tags in tag-table order, each with its own color.
    3. Add a per-entry `cover: false` flag, set it on `Android`, and skip flagged entries on the cover.
    4. Change WebGL wording in the header comment and the README to mobile.

    `LANGUAGES` and the parser stay unchanged.
  - **Verify:** `node Tools/PrintPDF/build.mjs <sample>.md --output <scratch folder>` builds a one-section sample, using every tag, both markers and an Optional block, with zero warnings. The cover lists the 10 stores and not `Android`.

- [ ] **B3. Validate the research files** (Depends on: B1 | Est: 30m)
  - **Context:** Decision 13. Agent output is unverified until checked.
  - **Scope & Entry:** `Documentation/Research/*.md`.
  - **Action:**
    1. Confirm that all 7 files follow the template and that every rule row has a URL.
    2. Confirm that every store has at least one official source or is marked partial.
    3. For every `must` rule that contradicts a seed fact or another group, open its source.
    4. Send a follow-up to the agent responsible for any missing store or section.
    5. Apply decision 4 to Epic, and set the "Checked on" date.
  - **Verify:**
    - A row count over `^\| \d+ \|` returns rows for all 7 files.
    - No rule row lacks `http`.
    - Every store in the tag table appears in at least one Sources list.

- [ ] **B4. Build the conflict matrix** (Depends on: B3 | Est: 45m)
  - **Context:** Decision 7. This step turns the store rules into rules that hold in every store.
  - **Scope & Entry:** `Documentation/Research/conflicts.md` (new).
  - **Action:**
    1. Group all rules by section and topic.
    2. For each topic, record either the strictest rule every store accepts (a main item) or one variant per store (tagged items), referencing rows as `<file>#<row>`.
    3. List every dropped rule with its reason: out of scope, duplicate or store page material.
    4. Map each Web 2.0.0 item to keep, adapt, drop or reverse (decision 15).
  - **Verify:** the number of referenced rows equals the total number of rule rows, and no topic has two contradicting main rules.

#### C. English checklist (Depends on: B | Est: 2h 30m)

- [ ] **C1. Draft the English checklist** (Depends on: B4 | Est: 2h)
  - **Context:** Decisions 7-12 and 15. The Web file is the structural template.
  - **Scope & Entry:** `Markdown/publishing-checklist.md` (new).
  - **Action:**
    1. Title it `# Unity Mobile Publishing Checklist`.
    2. Adapt the cover warning and the "How to read" list to per-store builds: main items apply to every build, a tagged item applies to its store's build, and `Android` covers every Android build.
    3. Write sections A-O from the matrix. Number items from 1 in each section, put human checks first, then `**Can be automated**`.
    4. Name MirraSDK5 in Unity hints where it applies.
    5. Finish with Sources: the official URLs from B3, "partial" marks, and "Checked on <date>".
  - **Verify:**
    - `node Tools/PrintPDF/build.mjs Markdown/publishing-checklist.md --language en --output Tools/PrintPDF/Output` finishes with zero warnings.
    - A one-line node check confirms that item IDs are unique and sequential within each section.
    - Every main and tagged entry in `conflicts.md` maps to an item.

- [ ] **C2. User review of the English draft** (Depends on: C1 | Est: 30m plus user time)
  - **Context:** Decision 11. A Russian translation is costly to redo, so the English text is frozen first.
  - **Scope & Entry:** `Markdown/publishing-checklist.md`, `Tools/PrintPDF/Output/publishing-checklist.pdf`.
  - **Action:** Send the PDF to the user, apply their feedback, and repeat until they approve.
  - **Verify:** The user approves in chat, and the PDF rebuilds with zero warnings.

#### D. Russian copy and repository docs (Depends on: C | Est: 1h 20m)

- [ ] **D1. Translate into Russian** (Depends on: C2 | Est: 1h)
  - **Context:** Decision 11.
  - **Scope & Entry:** `Markdown/publishing-checklist-russian.md` (new). Terms come from Web `Markdown/publishing-checklist-russian.md`.
  - **Action:** Translate item for item. Tags stay as they are; markers and section labels match `LANGUAGES.ru` exactly; the date line uses "Проверено".
  - **Verify:** A node check finds identical item ID lists in both files, and `node Tools/PrintPDF/build.mjs` with no arguments builds both PDFs with zero warnings.

- [ ] **D2. Write the README and CHANGELOG** (Depends on: D1 | Est: 20m)
  - **Context:** Decisions 4 and 8. Modelled on the Web `README.md` and `CHANGELOG.md`.
  - **Scope & Entry:** `README.md` and `CHANGELOG.md` (new).
  - **Action:**
    - README: a one-line description (10 stores, Android and iOS, covers the build and not the store page), a path table, build instructions, and the same 4 editing rules as Web.
    - CHANGELOG: `# Unity Mobile Publishing Checklist 1.0.0`, a summary of what is covered, and Epic's status under decision 4.
  - **Verify:** Both PDF covers show 1.0.0, and every README link resolves to an existing path.

#### E. Ship (Depends on: D | Est: 20m)

- [ ] **E1. Push and open the pull request** (Depends on: D2 | Est: 15m)
  - **Context:** Decision 17. Every outward step needs the user's go-ahead.
  - **Scope & Entry:** branches `main` and `feature/checklist-1.0.0`.
  - **Action:** Push `main`, push `feature/checklist-1.0.0`, and open the PR `feature: checklist 1.0.0` with a description listing sections, stores and sources. Squash merge only when the user says so.
  - **Verify:** `gh pr view` shows the PR against `main`, open, or merged after approval.

- [x] **E2. Rename the local folders** (Independent | Est: 5m)
  - **Context:** The user asked for the local renames right after A1. Windows locks a folder that is a running session's working directory.
  - **Scope & Entry:** `D:\github-mirragames-ai\PublishingChecklistAndroid`, `D:\github-mirragames-ai\AgentSkillsAndroid`.
  - **Action:** `AgentSkillsAndroid` was moved to `AgentSkillsMobile` directly. `PublishingChecklistAndroid` was copied to `PublishingChecklistMobile` (verified identical with `diff -r`), and the session moved into the copy. The old folder is a stale duplicate with no commits and is removed once no process holds it.
  - **Verify:** `git -C D:\github-mirragames-ai\PublishingChecklistMobile status` and `git -C D:\github-mirragames-ai\AgentSkillsMobile remote -v` succeed.
  - **Note:** Done on 2026-11-17, except removing the old folder: if `rm -rf D:\github-mirragames-ai\PublishingChecklistAndroid` still reports it busy, the user deletes it after closing this session.
