# Conflict matrix

Built in task B4 on 2026-11-17 from the 7 research files in this folder. Each research rule row is referenced as `<file>#<row>` and appears exactly once in this file: in a main item, a store-tagged item, or a drop.

- **main:** the rule holds in every build. The draft uses the strictest variant found across stores.
- **tag:** the rule holds only in the named store builds, so it becomes a store-tagged item. `Android` means all 8 Android builds.
- **drop:** no item. The reason is given: out of scope (decision 5), store form, Epic (decision 4), post-release metric, voluntary program, or covered by another topic.

A row is filed by its topic, so it can sit in a different section from the one its research file assigned. Draft wording is final only in `Markdown/publishing-checklist.md`.

## Fact checks

| Topic | Resolution | Evidence |
| --- | --- | --- |
| Amazon target API | Fire tablets run Fire OS 7 and 8 (API 28, 30). Fire OS 14 and 16 (API 34, 36) are Fire TV only, which is out of scope. | `technical#36` versus `samsung-amazon#43`; the device-filtering page labels both links "for Fire TV" |
| Samsung target API | 34 (Seller Portal notice) and 33 (Galaxy Games FAQ). Both are covered by the main item for API 36. | `samsung-amazon#28`, `technical` Samsung matrix row |
| Huawei 64-bit, target API | Only third-party sources exist. Both are covered by the main items for arm64-v8a and API 36. | `huawei-xiaomi#14` |
| 16 KB enforcement date | Google Play blocks non-compliant updates from 2027-02-01. Seed 2025-11-01 is corrected. | `google-play` and `technical` seed tables |
| Unity floor | 6000.0.68f1 or 6000.3.8f1, per plan decision 12. | `technical` "Unity versions" table |

## A. Build & performance

| Topic | Kind | Draft item | Rows |
| --- | --- | --- | --- |
| Stability | main | No crashes, freezes, force closes or ANRs in any flow: launch, tutorial, gameplay, ads, purchases, login, settings, rotation, rapid button presses, accessories plugged in or out. | apple#1, aptoide-epic#27, google-play#1, google-play#3, google-play#4, huawei-xiaomi#1, huawei-xiaomi#50, rustore-onestore#73, samsung-amazon#1, samsung-amazon#3, samsung-amazon#57 |
| Test devices | main | Each store build is tested on physical devices it ships to: iPhone and iPad, a Fire tablet, a Galaxy, a Xiaomi or Redmi and a Huawei phone. Android builds are also tested with no SIM card and no SD card. | samsung-amazon#2, samsung-amazon#56, huawei-xiaomi#49 |
| Release build | main | The build is the final release: not a development build, no placeholders, test data, debug menus, empty modules, unresponsive buttons or half-working features. | apple#2, huawei-xiaomi#7, huawei-xiaomi#51, samsung-amazon#5, samsung-amazon#6 |
| Live backends | main | Every backend the game uses is live during review, and the game never needs an update before it can be played. | apple#3, aptoide-epic#28 |
| Hidden features | main | No hidden or dormant features. Remote config may tune values, but never switches features on. | apple#5, huawei-xiaomi#44 |
| Loading | main | A loading screen shows at once. Any load longer than 15 seconds shows progress, and heavy loading runs after the first screen. | apple#10, samsung-amazon#58, samsung-amazon#61 |
| Content downloads | main | The first install is playable. Content needed before first play downloads only after the game shows its size and asks. Long downloads keep the device awake, and a failed download shows a message. | apple#11, apple#12, samsung-amazon#62 |
| Frame rate | main | Gameplay averages 55-60 fps and never drops below 25 fps for long on the weakest target device. | samsung-amazon#59, google-play#9 |
| Battery and heat | main | No fast battery drain or overheating: menus and idle screens cap the frame rate, one hour of play from 33 C ambient stays under 40 C, and no wake locks or work run in the background. | apple#9, huawei-xiaomi#52, samsung-amazon#4, samsung-amazon#60, google-play#5 |
| IPv6 | main | The game works on an IPv6-only network, with no hardcoded IPv4 addresses or IPv4-only APIs. | huawei-xiaomi#3, apple#71 |
| Memory | main, Auto test | Foreground memory stays under 2.25 GB on 4 GB RAM devices, and bitmap memory under 200 MB in the background. | google-play#6, google-play#7 |
| Code shrinking | main, Auto test | R8 shrinking is on when DEX code exceeds 50 MB. Unity: Minify Release with R8. | google-play#8 |
| No downloaded code | main, Ask AI | The game never downloads or runs code, installs APKs, updates itself or adds home screen shortcuts, and it is not a web-view wrapper. Downloads are data and assets only, and updates come only from the store. | apple#6, aptoide-epic#29, samsung-amazon#7, google-play#101, google-play#102, huawei-xiaomi#5, huawei-xiaomi#53, rustore-onestore#13 |
| Apple APIs | tag: Apple, Ask AI | Only public APIs and no deprecated frameworks; no SDK references UIWebView. | apple#7, apple#8 |
| Vulkan | drop: voluntary program | - | google-play#10 |
| Review notes | drop: store form | - | apple#4 |
| Epic binary | drop: Epic | - | aptoide-epic#40 |

## B. Advertisement

| Topic | Kind | Draft item | Rows |
| --- | --- | --- | --- |
| Ad presentation | main | Every ad is labeled as an ad, has a real, visible close button, and never imitates game UI, system dialogs or notifications. Non-rewarded full-screen ads can be closed within 15 seconds. | apple#15, aptoide-epic#31, google-play#13, google-play#15, google-play#17, huawei-xiaomi#24, rustore-onestore#33, rustore-onestore#67, samsung-amazon#8, samsung-amazon#64 |
| Ad placement | main | Interstitials show only at natural breaks. They never appear unexpectedly at the start of a level, before the loading screen, after every short action, when the player tries to exit, or where players tap for game controls. | google-play#11, google-play#12, google-play#16, huawei-xiaomi#25, huawei-xiaomi#70, samsung-amazon#65 |
| Ads inside the game only | main | Ads show only inside the running game: never on the home or lock screen, in notifications, in floating windows or after exit. No offerwalls. | apple#13, google-play#18, huawei-xiaomi#69 |
| No ad fraud | main, Ask AI | No invisible, hidden, stacked or auto-clicked ads, and the game is not built mainly to show ads. | google-play#22, apple#18 |
| No forced engagement | main | The game never forces an ad click or asks for personal data for ads. It never rewards installing another app, rating or reviewing. | google-play#19, apple#19, samsung-amazon#67 |
| Ad content rating | main, Ask AI | Every ad network and mediation adapter filters ad content to the game's 13+ rating or lower. No gambling, adult or political ads. | apple#14, google-play#20, google-play#21 |
| Ad reporting | main | Players can see why an ad was shown and report inappropriate ads without leaving the game, for example through the ad network's info screen. | apple#16, apple#17 |
| Cross-promotion | main, Ask AI | House ads and cross-promotion never show another store's name, badge or link (Web M24 inverted per build). | apple#20, huawei-xiaomi#28 |
| Promotional push | main | Promotional notifications go only to players who opted in inside the game, and the game has an opt-out. | apple#21, huawei-xiaomi#72, rustore-onestore#40 |
| Rewarded opt-in | main, Optional rewarded block | A rewarded ad starts only after the player taps a button that names the reward (Web B12). | google-play#14 |
| Close button timing | tag: Huawei | Close buttons are visible from the start and never wait for a countdown. Closing an ad never opens another ad. | huawei-xiaomi#26 |
| Ad clicks | tag: Huawei | Ads open links only after a tap on their own click area, never on shake or swipe, and never install apps by themselves. | huawei-xiaomi#27 |
| Ads in Russia, Huawei | tag: Huawei | In Russia, Petal Ads uses SDK 4.60.301+ with ERIR registration and an advertiser-information button. | huawei-xiaomi#29, technical#77 |
| Ad networks in Russia | tag: RuStore | Ads come from networks that serve Russia, such as Yandex Mobile Ads or VK Ads. AdMob serves no users in Russia and no publishers based in Russia or Belarus. | rustore-onestore#35, technical#71, technical#72 |
| Ad disclosure | tag: RuStore | The game tells players it shows ads. The privacy policy lists the ad SDKs, the data passed and the purposes, and every ad SDK is declared in the console. | rustore-onestore#32, rustore-onestore#34 |
| Ads without Google services | tag: Huawei, Amazon | Every ad network and adapter loads, shows and closes ads on a device without Google Play services. Builds use the full AdMob SDK, not Lite, and only Fire-compatible networks on Amazon. | samsung-amazon#66, technical#69, technical#70, technical#76 |
| AdMob registration | tag: Xiaomi | The AdMob app is registered with the store "Xiaomi GetApps" and app-ads.txt is set up. | huawei-xiaomi#71 |
| Epic promotional content | drop: Epic | - | aptoide-epic#50 |

## C. In-app purchases (Optional)

| Topic | Kind | Draft item | Rows |
| --- | --- | --- | --- |
| Store billing only | main, Ask AI | Each store build sells digital items only through that store's billing: Google Play Billing, StoreKit, Huawei IAP, Samsung IAP, Xiaomi GetApps IAP, RuStore Pay SDK, ONE store IAP, Amazon IAP or Aptoide Billing. The build has no links, buttons or text leading to another payment method. Bought currency never expires and is spent only in this game. | apple#22, apple#27, google-play#25, google-play#26, google-play#33, samsung-amazon#68, rustore-onestore#43, rustore-onestore#47, huawei-xiaomi#61, huawei-xiaomi#62, aptoide-epic#16, technical#57 |
| Free core game | main | The game charges nothing at first use, and its main functions are never locked behind payment (Web C1). | huawei-xiaomi#68, huawei-xiaomi#23 |
| Prices | main | Prices come from the store's product data in local currency (rubles on RuStore, KRW in Korea) and match the payment screen. No hard-coded prices. | aptoide-epic#20, google-play#32, huawei-xiaomi#20, rustore-onestore#45, rustore-onestore#28 |
| Random items | main | No paid random items: no loot boxes, gacha or random rewards bought with money or with currency that can be bought (plan decision 19). Every paid item shows exactly what the player gets, which also meets the odds rules. | apple#25, google-play#34, huawei-xiaomi#22, samsung-amazon#15, samsung-amazon#72 |
| Subscriptions | main | Subscriptions, if any, last at least 7 days, keep giving value, and show price, period, auto-renewal and how to cancel before purchase. | apple#28, apple#29, google-play#35 |
| Testable products | main | Every product configured in the store can be bought and is delivered in the submitted build, and has been tested in that store's sandbox or test mode. | apple#26, aptoide-epic#21, aptoide-epic#26, rustore-onestore#74, samsung-amazon#16 |
| Billing unavailable | main | If billing is unavailable (country not supported, store app missing, outdated or signed out), the shop shows a clear message or hides itself, and the game keeps working (Web C2, C7). | huawei-xiaomi#66, technical#62 |
| Restore | main | Settings have a Restore Purchases button for non-consumables and subscriptions. Purchases completed while the game was closed, or outside it, are delivered at launch and on return to the game, exactly once (Web C13, C14). | apple#23, google-play#31, samsung-amazon#13, rustore-onestore#46 |
| Pending purchases | main, Auto test | Items are granted only for completed purchases, never pending ones, and the player sees that a payment is still pending. | google-play#30 |
| Confirmation | main, Auto test | Every purchase is verified, server-side where the store offers it, then consumed or acknowledged at once, and within 48 hours at most (Aptoide 48 h; Google Play and ONE Store 3 days). | google-play#29, aptoide-epic#22, aptoide-epic#23, samsung-amazon#14, huawei-xiaomi#64 |
| Google Play billing | tag: Google Play, Auto test | Play Billing Library 8 or newer, with its version meta-data kept in the merged manifest. Move to version 9 before 2027-08-31. Unity: Unity IAP 4.14.0+ or 5.0.0+; 5.4.0+ for PBL 9. | google-play#27, google-play#28, google-play#41, technical#55, technical#56 |
| Apple billing | tag: Apple, Ask AI | StoreKit 2 through Unity IAP 5. With a minimum iOS below 15, use Unity IAP 5.1.0+ and test on iOS 13 or 14. Restore through AppStore.sync only after a tap. Receipt checks accept the SHA-256 certificate. | apple#24, apple#30, apple#31, technical#65, technical#66 |
| Huawei billing | tag: Huawei | Purchases use HUAWEI IAP. Subscriptions never auto-renew by default, and the purchase page shows the renewal terms and how to cancel. | huawei-xiaomi#19, huawei-xiaomi#21 |
| Samsung billing | tag: Samsung, Auto test | Samsung IAP 6.x (Unity plugin 6.5.2) in production mode, with no Samsung IAP 4.x left in the manifest. GetOwnedList runs at every launch. Unity: Minimum API Level 23+. | samsung-amazon#9, samsung-amazon#10, samsung-amazon#11, samsung-amazon#12, technical#63 |
| Xiaomi billing | tag: Xiaomi | GetApps IAP SDK 1.1.8+ from an enterprise account. Every purchase passes a stable, unique obfuscatedAccountId of at most 200 characters. | huawei-xiaomi#63, huawei-xiaomi#65, huawei-xiaomi#67 |
| RuStore billing | tag: RuStore | RuStore Pay SDK, not the retired BillingClient SDK. Every payment method is declared in the console. Two-step payments are confirmed within 6 hours, and the flow works without RuStore installed. Unity: Activity is UnityPlayerActivity (GameActivity breaks payments), Minimum API Level 24, plus the console app ID and a unique deeplink scheme. | rustore-onestore#27, rustore-onestore#29, rustore-onestore#30, rustore-onestore#31, technical#60 |
| ONE Store billing | tag: ONE Store | ONE store IAP SDK 21.04.00 with the required queries tag, and no dev_option meta-data in the release. The game asks the player to update or sign in to ONE store when billing requests it. Server checks send x-market-code. No subscriptions in the global build. | rustore-onestore#44, rustore-onestore#52, rustore-onestore#54, rustore-onestore#75, technical#61 |
| ONE Store external payment | drop: covered by "Store billing only" | With ONE Store's third-party payment or a ONEshop webshop, the API reporting, receipt ID and webshop separation rules apply. Not planned: the checklist uses ONE store IAP. | rustore-onestore#48, rustore-onestore#49 |
| Korea cancellation | tag: ONE Store | In Korea, every item that cannot be cancelled is marked as non-cancellable before purchase. | rustore-onestore#72 |
| Amazon billing | tag: Amazon | Amazon Appstore SDK 3.0.9, not Unity IAP 5 and not the unsupported Billing Compatibility SDK. Unity plugin 3.0.2 is 32-bit only, so the ARM64 build needs a custom bridge to SDK 3.0.8+, and purchases are tested on ARM64. | samsung-amazon#69, samsung-amazon#70, samsung-amazon#71, technical#58, technical#59 |
| Aptoide billing | tag: Aptoide | Aptoide Billing SDK replaces Play Billing, is initialized with the console public key, stays in every update, and completes purchases without the Aptoide Wallet app. Unity: the Aptoide Unity billing plugin, Android files only once in Assets/Plugins/Android. | aptoide-epic#17, aptoide-epic#18, aptoide-epic#19, aptoide-epic#24, aptoide-epic#25, technical#64 |
| Alternative billing programs | drop: optional programs, not used | The main item forbids external payment links in every build. | google-play#36, google-play#37, google-play#38, google-play#39, google-play#40 |
| Epic purchases | drop: Epic | - | aptoide-epic#53, aptoide-epic#54 |

## D. User data

| Topic | Kind | Draft item | Rows |
| --- | --- | --- | --- |
| Save durability | main | Progress, purchases, settings and sign-in survive a restart, an update and backgrounding (Web D1, D2). | samsung-amazon#73 |
| Restore on a new install | main | Progress can be restored after a reinstall or on a new device, through cloud saves or login. Player identity is never keyed to ANDROID_ID, which differs between store builds signed with different keys. | technical#29, technical#26, google-play#48 |
| Guest play | main | Guest play is the default. Single-player content needs no login, and no personal data (name, email, birthday) is mandatory (Web D3, D4). | apple#34 |
| Login works | main, Optional login block | Account creation and sign-in work end to end in every store build. | aptoide-epic#30, huawei-xiaomi#37, huawei-xiaomi#84 |
| Login choice | main, Optional login block | Login never depends on a single third-party provider: the game's own or the store's account also works. On iOS, any third-party login is matched by Sign in with Apple. | apple#35, rustore-onestore#26 |
| Account deletion | main, Optional login block | If players can create an account, Settings has a Delete account option. It deletes the account and its personal data, not just deactivates it, within 15 working days and without contacting support, and it says what is kept and for how long. | apple#32, apple#33, google-play#43, google-play#45, huawei-xiaomi#36, rustore-onestore#25 |
| Deletion web page | main, Optional login block | A web page lets players request account deletion without the game. Its URL goes into the hand-off list. | google-play#44, samsung-amazon#75 |
| Apple login | tag: Apple, Optional login block | Social logins can be revoked inside the game, social tokens never leave the device, and Sign in with Apple relay addresses on both domains are accepted. | apple#36, apple#37 |
| Login without Google services | tag: Huawei, Amazon | Login uses a provider that works without Google Play services, with no Google Sign-In. | samsung-amazon#74 |
| Game service IDs | tag: Google Play, Apple | Play Games Services and Game Center player IDs are never the primary account identity, and Game Center IDs are never shown or shared. | google-play#47, apple#38 |
| Data in Russia | tag: RuStore | Personal data of players in Russia (accounts, cloud saves, analytics profiles) is stored in databases located in Russia. The law (152-FZ) applies to Russian players in every build, and RuStore enforces it. | rustore-onestore#24 |
| Review test accounts | drop: store form | Guest play makes them unnecessary. | google-play#46, samsung-amazon#17, samsung-amazon#76 |
| Restore Credentials | drop: games excluded by Google | - | google-play#49 |
| Epic EULA | drop: Epic | - | aptoide-epic#51 |

## E. Analytics & events

| Topic | Kind | Draft item | Rows |
| --- | --- | --- | --- |
| Analytics consent | main | Analytics data is collected only with the player's consent, is used only for the purpose consented to, and the player can withdraw consent in Settings. Personal data goes to third parties, AI services included, only with explicit permission. | apple#39, apple#42, apple#43 |
| Analytics without Google services | tag: Huawei, Amazon | Analytics and crash reporting work without Google Play services: only Firebase libraries that need no Play services, or SDKs verified on a Fire tablet. | samsung-amazon#77, technical#94 |

## F. Controls

| Topic | Kind | Draft item | Rows |
| --- | --- | --- | --- |
| Back | tag: Android | The Back gesture and button close the top popup, pause, or ask to exit on the main screen. They never force-close the game, and no screen traps the player. Unity: Predictive Back Gesture Support on, because with target API 36 Android 16 no longer sends the old Back event. | google-play#54, huawei-xiaomi#8, samsung-amazon#18, samsung-amazon#78, technical#50 |
| System behavior | main | The game never changes system settings or standard buttons: volume buttons, silent switch, Bluetooth, GPS, restart. | apple#45 |
| Touch targets | main | Touch targets are at least 7 mm (44 pt) with hit areas matching their graphics, and text is at least 11 pt. | apple#46, samsung-amazon#79 |
| Controllers, PC | drop: voluntary program; PC out of scope | Device availability (section N) keeps Google Play Games on PC off. | google-play#55, google-play#56 |

## G. User interface

| Topic | Kind | Draft item | Rows |
| --- | --- | --- | --- |
| Full screen | main | The game fills the whole screen on every phone and tablet aspect ratio without stretching (Web G1, G2). | samsung-amazon#80, apple#48 |
| Safe area | main | The game draws edge to edge, and HUD, buttons and banners stay inside the safe area: notch, Dynamic Island, cutouts, status and navigation bars, home indicator. Unity: Screen.safeArea; "Render outside safe area" does nothing on Android 15+. | apple#49, google-play#57, technical#45, technical#46 |
| Resizing | main | Rotation, folding, split screen and window resizing re-lay out the UI without stretching, clipping or losing state, and the game respects the device's orientation lock. | technical#49, apple#53, samsung-amazon#19, samsung-amazon#81, google-play#59 |
| Game category | tag: Android, Auto test | The merged manifest declares android:appCategory="game", so Android 16 keeps the game's orientation on tablets and foldables. Unity 6: App Category = Game. | google-play#58, technical#47, technical#48 |
| Store identity | main | The installed name and icon match the store listing. There is exactly one launcher icon, it does not look like a system icon, and there are no fake badges (Web G16). | huawei-xiaomi#39, huawei-xiaomi#82, rustore-onestore#9, samsung-amazon#20 |
| Support contact | main | Settings show a support contact, such as an email address or page (Web M15 inverted). | huawei-xiaomi#38 |
| Apple layout | tag: Apple | The iPhone game also runs on iPad. The iPad build declares all four orientations, does not rely on UIRequiresFullScreen, and is tested on iPhone Duo. | apple#56, apple#55, apple#52, apple#54 |
| Launch screen | tag: Apple, Auto test | Info.plist has a launch screen key, or iOS 27 SDK uploads fail with ITMS-90870. | apple#47 |
| ONE Store orientation | tag: ONE Store | Orientation stays locked while the ONE store purchase screen is open. | rustore-onestore#76 |

## H. Localization

| Topic | Kind | Draft item | Rows |
| --- | --- | --- | --- |
| English | main, Ask AI | English is included and is the default and fallback language (Web H5). | huawei-xiaomi#18, huawei-xiaomi#81 |
| Russian | main, Ask AI | Russian is included in full, for every player-facing text (Web H6). Russian law 168-FZ has required it since 2026-03-01. | rustore-onestore#20, rustore-onestore#21 |
| Apple purpose strings | tag: Apple, Ask AI | Every Info.plist purpose string is translated into each supported language. | apple#57 |
| Locale codes | tag: Android, Ask AI | Language detection accepts the locale codes he, yi and id, which API 35 no longer converts to iw, ji and in. | technical#54 |

## I. Audio

| Topic | Kind | Draft item | Rows |
| --- | --- | --- | --- |
| Silent mode | main | The device's mute switch or silent mode silences the game (Web I5). | samsung-amazon#21, samsung-amazon#82 |
| Interruptions | main | Audio stops for calls, sleep and backgrounding, and resumes correctly afterwards (Web I7). | samsung-amazon#22, apple#59 |
| Apple audio session | tag: Apple | The audio session uses the Ambient or Solo Ambient category, and Info.plist declares no unused background modes. | apple#58, apple#60 |
| Android audio focus | tag: Android | Audio focus is requested only in the foreground and released when another app plays audio. | technical#51 |

## J. Pause

| Topic | Kind | Draft item | Rows |
| --- | --- | --- | --- |
| Lifecycle | main | Leaving the game (Home, a call, a notification, the app switcher, settings, an external link) pauses it and saves state. Returning restores it with no lost progress (Web J1, J6). | apple#61, samsung-amazon#83 |
| Notifications optional | main | The game works fully with notifications denied. | apple#62 |
| No background work | main, Ask AI | No foreground services, full-screen intents, exact alarms, floating windows, auto-start, lock-screen or launcher changes, blocking of other apps' ads, or bypassing of power management. | google-play#60, google-play#61, google-play#62, google-play#63, huawei-xiaomi#9, samsung-amazon#93 |
| Update prompts | main | No in-game update or reboot prompts; updates come only from the store. Xiaomi bans them, and Huawei rejects blocking ones. | huawei-xiaomi#83, huawei-xiaomi#6 |
| RuStore update SDK | drop: optional, conflicts with the Xiaomi ban | Prompts are banned in every build by the main item above. | rustore-onestore#41 |

## K. Social interactions (Optional)

| Topic | Kind | Draft item | Rows |
| --- | --- | --- | --- |
| No rating incentives | main | The game never requires a rating or review, never blocks content until one is given, and never rewards one (Web K4). | apple#64, google-play#66, huawei-xiaomi#40, huawei-xiaomi#75, rustore-onestore#36, samsung-amazon#85 |
| Rating prompt | main | The rating prompt is the store's own review dialog, shown after a success such as a finished level. It never appears on first launch, mid-level, or as a direct result of a button tap, and there is no "Do you like the game?" pre-question. A "Rate us" button opens the store page instead. | apple#63, apple#66, apple#67, google-play#64, google-play#65 |
| Store review APIs | main | Each build uses its own store's review API: Play In-App Review, StoreKit requestReview (not SKStoreReviewController), AppGallery in-app comments, Galaxy Store Review Broadcast, or the RuStore Review SDK at most once a day. Aptoide, Xiaomi, ONE Store and Amazon builds only open their store page. | apple#65, huawei-xiaomi#41, samsung-amazon#23, rustore-onestore#37, aptoide-epic#38 |
| Own-store links | main, Ask AI | Rate us, more games and cross-promotion links open the store the build is for, and never another store (Web M24 inverted). | rustore-onestore#19, rustore-onestore#66, samsung-amazon#84, huawei-xiaomi#74 |
| Sharing | main | Sharing sends nothing until the player confirms the content and recipients. It shares only game images or text, with no QR codes or download links, and fails with a message when the needed app is missing. | google-play#69, huawei-xiaomi#73, samsung-amazon#87 |
| Game Center | tag: Apple, Auto test | If the game uses Game Center, the build has the Game Center entitlement and its features are configured in App Store Connect. | apple#68, technical#93 |
| Play Games Services | tag: Google Play | If used, Play Games Services is the v2 SDK, signs in automatically at launch, and gameplay continues when sign-in fails. | google-play#67, google-play#68 |
| Game services without Google | tag: Huawei, Amazon | Leaderboards, achievements and cloud saves use the game's own or a GMS-free backend, never Play Games Services. | samsung-amazon#86 |
| Achievement count | drop: voluntary program | - | google-play#70 |

## L. Multiplayer (Optional)

| Topic | Kind | Draft item | Rows |
| --- | --- | --- | --- |
| Player content | main | Chat, names, avatars and other player content have rules players accept before use, filtering, in-game reporting of content and players, blocking, and a published moderation contact (Web L3, L4). Chat with strangers is never the main feature. | apple#69, apple#70, google-play#71, huawei-xiaomi#48, huawei-xiaomi#89, rustore-onestore#38, samsung-amazon#27 |
| Recording | main | Voice chat, camera and gameplay recording ask for consent first and show an indicator while recording. | apple#72 |
| Secure connections | main, Auto test | Every network endpoint (backend, multiplayer, ads, analytics, purchase checks) uses TLS 1.2 or newer: HTTPS and WSS (Web L13). Personal data never travels unencrypted. | technical#52, google-play#109 |
| Amazon age check | tag: Amazon | Chat and other player content sit behind an age check. | samsung-amazon#89 |
| Chat in Russia | tag: RuStore | If chat makes the studio an information distribution organizer (149-FZ), the studio is registered with Roskomnadzor and keeps chat data as 374-FZ requires. | rustore-onestore#39 |
| Chat in Korea | tag: ONE Store | In Korea, chat rooms show caution and sanction notices and warn players not to share bank, ID or card numbers. | rustore-onestore#71 |
| LAN play | tag: Android | LAN multiplayer, if any, declares NEARBY_WIFI_DEVICES and works with the local-network restriction on. From API 37 it needs a Play Console declaration. | google-play#72, technical#53 |
| Epic player content | drop: Epic | - | aptoide-epic#49 |

## M. Content & links

| Topic | Kind | Draft item | Rows |
| --- | --- | --- | --- |
| Distinct product | main | Each game is a distinct product with real, lasting gameplay. It is not a reskin or near-identical template of another studio title in the same store, and not a repackaged website. | apple#75, apple#76, google-play#79, google-play#2, aptoide-epic#32 |
| Licensed content | main | All code, art, music, sounds, fonts and names are original or licensed, with proof ready on request. No trademarks, celebrities, or other games' or brands' characters and look, and no implied link to the store or a device maker (Web M11-M13). | apple#74, google-play#77, google-play#78, huawei-xiaomi#46, rustore-onestore#18, rustore-onestore#65, samsung-amazon#24, samsung-amazon#26, samsung-amazon#92 |
| Other platforms | main, Ask AI | The game names only its own store and platform: no other store's, platform's or device brand's name, logo or badge. For example, no "Google Play" or "Android" in the iOS build. | apple#73, huawei-xiaomi#42 |
| Prohibited content | main | No sexual content, profanity, graphic violence, hate, self-harm, drugs, alcohol or tobacco, or offence to religions, ethnicities or real people (Web M2-M4). | aptoide-epic#33, google-play#76, huawei-xiaomi#78, samsung-amazon#88 |
| Russian content law | tag: RuStore | No justification of extremism or Nazism, LGBT "propaganda" (398-FZ), discrediting of the Russian army or state symbols, drugs as a mechanic, new depictions of alcohol or tobacco use, or mockery of real tragedies. | rustore-onestore#14, rustore-onestore#15 |
| No gambling | main | No real-money gambling, betting, or paid entry to win money or prizes. Simulated gambling never points to real gambling. Contests, if any, are run by the studio, with in-game rules saying the store is not involved (Web M8). | google-play#74, google-play#75, huawei-xiaomi#77, rustore-onestore#16, rustore-onestore#64, apple#81 |
| 13+ rating | main | Content keeps every store rating at 13+ or lower: simulated gambling is at most infrequent, there is no free web browser, and there are no paid loot boxes, which raise the Apple and Huawei ratings to 16+ in Australia and 18+ in Brazil. The content facts that rating questionnaires ask about go into the hand-off list. | apple#77, apple#78, apple#79, apple#80, google-play#73, huawei-xiaomi#45, huawei-xiaomi#79, rustore-onestore#17, rustore-onestore#42, rustore-onestore#63, samsung-amazon#90 |
| Not for children | main | Nothing suggests the game targets children: no "for kids" wording, and no imagery or characters that make it look made for kids (decision 6). | google-play#81, huawei-xiaomi#47 |
| Age laws | main | Where law requires age checks (US states with app store age laws, Brazil, Korea), the game reads the store's age signal and restricts the affected features itself. Player-made levels above the game's rating can be identified and restricted by age. | google-play#42, rustore-onestore#77, apple#82 |
| Korea probability items | drop: no paid random items (decision 19) | In Korea, each probability item type is labelled, its odds are shown as percentages on the purchase, inquiry and use screens and published on the website, and ads say "includes probability items". | rustore-onestore#60, rustore-onestore#61, rustore-onestore#62 |
| No app distribution | main | The game offers no downloads of other apps, has no app-market functions, and never pushes players to install or open another app or market. | huawei-xiaomi#43, huawei-xiaomi#76, samsung-amazon#25 |
| Device security | main, Ask AI | The game never asks players to turn off Play Protect or other device security. | google-play#82 |
| No interactive AI | main | No interactive generative AI in the game (Web M6), so Google Play's reporting rule for AI content does not arise. | google-play#80 |
| Listing features | drop: store page material | - | samsung-amazon#91 |
| Xiaomi content clause | drop: contract term, no build impact | - | huawei-xiaomi#80 |
| Epic content and rating | drop: Epic | - | aptoide-epic#41, aptoide-epic#42, aptoide-epic#43, aptoide-epic#44, aptoide-epic#45, aptoide-epic#47, aptoide-epic#48, aptoide-epic#52 |

## N. Store builds

| Topic | Kind | Draft item | Rows |
| --- | --- | --- | --- |
| Unity floor | main | Unity 6000.0.68f1+ or 6000.3.8f1+. 2022.3 lost public support on 2025-05-30, bundles no AGP 8 (needed for 16 KB packaging and Yandex Ads 8.6), and has UIScene support only in xLTS. | technical#95, technical#73, technical#74, technical#75 |
| Store SDK isolation | main, Ask AI | Each store build contains only its own store's SDKs: billing, login, review, update, push and game services. No HMS or agconnect libraries outside the Huawei build, and no other store's SDK in the Google Play build (decision 2). | google-play#100, huawei-xiaomi#16 |
| Builds without Google services | tag: Huawei, Amazon | The full core loop (play, saves, purchases, ads) works on a device without Google Play services. There is no SDK that needs them: no Play Billing, Google Sign-In, Play Games Services, FCM, Play Integrity or Play review/update. Push uses HMS Push or Amazon Device Messaging. | huawei-xiaomi#2, samsung-amazon#46, samsung-amazon#47 |
| Target API | main, Auto test | Every Android build targets API 36, which also meets Samsung (34), Amazon (30) and every other store. | google-play#84, google-play#85, technical#1, technical#2, technical#3, samsung-amazon#28, technical#8, samsung-amazon#43, technical#36, aptoide-epic#12, huawei-xiaomi#15 |
| Minimum API | main, Auto test | minSdkVersion is 24 to 28: 24 or higher for current ad and billing SDKs (AdMob 25.5+, RuStore Pay, Samsung IAP 6, Play Billing 8.1+), and at most 28 so Fire OS 7 tablets and Android 8.0 (RuStore's minimum) stay covered. compileSdk is 35 or higher. Unity: 6000.3 sets 25 as the lowest. | technical#67, technical#68, samsung-amazon#44, google-play#103, rustore-onestore#1 |
| ABIs | main, Auto test | Every Android build ships arm64-v8a and armeabi-v7a, because some Fire tablets are 32-bit only. Unity: IL2CPP, Target Architectures ARMv7 and ARM64. | google-play#86, technical#7, huawei-xiaomi#14, samsung-amazon#29, technical#9, samsung-amazon#45 |
| 16 KB pages | main, Auto test | Every native library, Unity's and each SDK's (Burst 1.8.21+), is 16 KB aligned. zipalign -P 16 passes, and the game runs on a 16 KB device or emulator without the compatibility warning. Unity: 6000.0.45f1+ (AGP 8.7). Google Play blocks updates without it from 2027-02-01. | google-play#87, google-play#88, google-play#89, technical#10, technical#11, technical#12, technical#13, technical#14, technical#15, technical#16, samsung-amazon#30 |
| Release signing | main, Auto test | The release is not debuggable, is signed with a release key using APK Signature Scheme v2 (plus v1), declares android:exported on every component with an intent filter, uses no code packers, and has a versionName under 50 characters. | google-play#95, huawei-xiaomi#4, rustore-onestore#3, samsung-amazon#51, technical#25, rustore-onestore#57 |
| Package name | main | One final package name for every Android build. It matches the package entered in each store console and never changes. | google-play#94, aptoide-epic#3, huawei-xiaomi#12, huawei-xiaomi#56 |
| Signing plan | main | Every Android build is signed with the same studio-held app signing key. Google Play App Signing uses the studio's uploaded key, not a Google-generated one. Store-managed signing (Samsung or Huawei AAB, ONE Store) receives the same key, or the build is a studio-signed APK. Amazon re-signs, so its certificate hashes go wherever signatures are checked. This meets Aptoide's same-signature rule for games with purchases and Xiaomi's and RuStore's preference. | aptoide-epic#4, aptoide-epic#5, aptoide-epic#8, huawei-xiaomi#57, rustore-onestore#6, rustore-onestore#7, technical#42, technical#44, rustore-onestore#58, samsung-amazon#32, technical#30, google-play#92, technical#32 |
| Amazon signature | tag: Amazon | Login keys, anti-tamper checks and SDK key hashes use Amazon's re-signed certificate hashes from the Developer Console. | samsung-amazon#50, technical#37 |
| Separate Samsung package | drop: conflicts with the signing plan | Aptoide requires the Google Play package and signature for games with purchases. | samsung-amazon#33 |
| Version codes | main, Auto test | versionCode rises with every release, is never reused, stays at or below 2100000000, and every non-Play build's code is higher than the Play build's (for example a store digit prefix), so Google Play never silently replaces another store's build. | google-play#93, aptoide-epic#6, aptoide-epic#7, huawei-xiaomi#13, huawei-xiaomi#55, rustore-onestore#5, technical#40, samsung-amazon#52, huawei-xiaomi#17 |
| Cross-store install | main | QA installs each store build over every other store's build. The result matches the signing plan, and on Android 14+ an update from a second store shows the approval prompt and keeps the save. | technical#27, technical#28 |
| No installer check | main | No build blocks installs from other stores: Google Play's automatic installer check is off in Play Console, and no build gates play on Play Integrity. | aptoide-epic#9, rustore-onestore#2 |
| Developer verification | main | Every package name and every signing certificate used by any store build, including the certificates of stores that re-sign, is registered for Android developer verification, and keystores are backed up. Since 2026-09-30, unregistered apps cannot be installed from Google Play, Samsung or Xiaomi in Brazil, Indonesia, Singapore and Thailand, and enforcement extends worldwide in 2027. | google-play#96, google-play#97, aptoide-epic#10, huawei-xiaomi#60, samsung-amazon#34, technical#17, technical#18, technical#19, technical#20, technical#21, technical#22, technical#23, technical#24, rustore-onestore#59 |
| SDK health | main, Auto test | No SDK version that Google's SDK Index marks as policy-violating or outdated for more than 90 days. | google-play#98, google-play#99 |
| Google Play package | tag: Google Play, Auto test | AAB with no OBB; large content goes through Play Asset Delivery within its limits (base module 500 MB, asset packs 1.5 GB each, 4 GB install-time total). | google-play#83, google-play#90, technical#4, technical#5, technical#6 |
| Other Android packages | main, Auto test | Every non-Play Android build is a universal APK of 2 GB or less (ONE Store's cap) with no OBB files and no fast-follow or on-demand asset packs. Content beyond that downloads in the game. Unity: Build App Bundle off, Split Application Binary off. | aptoide-epic#1, aptoide-epic#2, huawei-xiaomi#54, huawei-xiaomi#10, huawei-xiaomi#11, rustore-onestore#55, rustore-onestore#56, samsung-amazon#48, samsung-amazon#49, samsung-amazon#31, rustore-onestore#4, technical#31, technical#33, technical#34, technical#35, technical#38, technical#39, technical#41, technical#43 |
| Initial download | main | The initial download stays at or below 200 MB, where Google Play and iOS start asking before mobile-data downloads. | google-play#91, apple#87 |
| ONE Store manifest | tag: ONE Store, Auto test | The manifest has the ONE store queries, and the release has no dev_option meta-data or SDK log level calls. The global build is one binary using IAP SDK V19+ and ONE store app signing. | rustore-onestore#50, rustore-onestore#51, rustore-onestore#53 |
| Simultaneous updates | main | Every store build is released together at the same version, so no store lags behind. Aptoide and RuStore may remove builds that fall behind other stores for a year. | aptoide-epic#15, rustore-onestore#8 |
| Device availability | main | Phones and tablets only: Google Play Games on PC, Apple silicon Mac and Apple Vision Pro availability are turned off, and unsupported devices are excluded in each console, not in code. | google-play#104, google-play#105, apple#92, apple#93 |
| Amazon devices | tag: Amazon | The Fire build targets Fire tablets only. Hardware features implied by permissions are android:required="false", there are no wallpaper, widget or lock-screen features, and hardware acceleration is on. Alexa tablets get the Google Play build. | samsung-amazon#41, samsung-amazon#42, samsung-amazon#53, samsung-amazon#54, samsung-amazon#55 |
| Xiaomi signature check | tag: Xiaomi | For a game that is not on Google Play, the console's empty verification APK keeps its name and package, is signed with the game's key using v2 or v3, and is at most 4 MB. "Auto update" from Google Play is off, because the Xiaomi build differs from the Play build. | huawei-xiaomi#58, huawei-xiaomi#59 |
| Samsung countries | tag: Samsung | Vietnam is excluded from distribution countries for games. | samsung-amazon#35 |
| Apple toolchain | tag: Apple, Auto test | Built with Xcode 26+ and the iOS 26 SDK (Xcode 27 and the iOS 27 SDK from April 2027), with UIScene life cycle support, and native plug-in callbacks tested after the UIScene migration. Unity: 6000.0.68f1+ or 6000.3.8f1+. | apple#83, technical#89, apple#50, apple#51, technical#92 |
| Apple target | tag: Apple, Auto test | The deployment target is iOS 15 or later (App Store minimum 13), and UIRequiredDeviceCapabilities lists only what the game cannot run without. | apple#84, technical#90, technical#91, apple#88 |
| Apple package | tag: Apple, Auto test | The app is at most 4 GB uncompressed with at most 500 MB of __TEXT, has no On-Demand Resources and no bitcode, sets ITSAppUsesNonExemptEncryption, and is uploaded with matching bundle ID and a unique build number. | apple#85, apple#86, apple#89, apple#90, apple#91 |
| Hand-off list | main | Each store build ships with a hand-off list for the store forms: every SDK and its version and compliance, permissions, data collected or shared and why, the Advertising ID, ads present, purchases, loot boxes, chat, data sent abroad, and the privacy policy and account deletion URLs. Data safety, privacy labels, ads declarations and rating questionnaires are filled from it. | google-play#23, apple#44, google-play#50, google-play#108, samsung-amazon#38, samsung-amazon#97, google-play#115, aptoide-epic#37, rustore-onestore#70, google-play#110 |
| Aptoide account | drop: account step, games are free | Aptoide subscription and ownership verification are one-time account steps, and studio games are free to download. | aptoide-epic#11, aptoide-epic#13, aptoide-epic#14 |
| Epic builds | drop: Epic | - | aptoide-epic#39, aptoide-epic#55, aptoide-epic#56, aptoide-epic#57, aptoide-epic#58 |

## O. Privacy & permissions

| Topic | Kind | Draft item | Rows |
| --- | --- | --- | --- |
| Privacy policy | main | Settings and the first-run consent screen link the privacy policy, in English and Russian, at the same URL as every store console. It covers the data collected, purposes, every SDK that receives data, retention, deletion, consent withdrawal and a contact (Web M14 inverted). | apple#94, google-play#106, huawei-xiaomi#30, samsung-amazon#36, samsung-amazon#94, aptoide-epic#35, rustore-onestore#22 |
| Consent screen | main | On first launch, before any SDK collects personal data, a consent screen says what is collected and why, with equally prominent Agree and Reject buttons and nothing pre-checked. Consent is separate from terms of use and can be changed in Settings. | huawei-xiaomi#31, google-play#107, samsung-amazon#95, huawei-xiaomi#88, huawei-xiaomi#85, rustore-onestore#69, rustore-onestore#23 |
| Personalized ads switch | main | Settings have a switch that turns personalized ads off and takes effect. | huawei-xiaomi#32 |
| Ad consent standards | main, Auto test | Builds with AdMob show a Google-certified CMP (IAB TCF v2.3 with disclosedVendors) before personalized ads in the EEA, UK and Switzerland, and send US state privacy signals (GPP or RDP). | technical#82, technical#83, technical#84 |
| No permission incentives | main | No feature, reward or content depends on allowing tracking, notifications, location or other permissions. | apple#98 |
| Permissions in context | main | No permission is requested at first launch. Each one is asked when its feature is used, with its purpose shown, and a denial never blocks play, sign-in or causes repeated prompts. | apple#102, google-play#111, huawei-xiaomi#34, rustore-onestore#12 |
| Manifest permissions | tag: Android, Auto test | The merged manifest, SDK additions included, holds only permissions a feature needs. None of: QUERY_ALL_PACKAGES, MANAGE_EXTERNAL_STORAGE, broad media or contacts access, READ_LOGS, SYSTEM_ALERT_WINDOW, phone or SMS, accessibility or device admin, REQUEST_INSTALL_PACKAGES, or location for ads or analytics. | google-play#112, google-play#113, google-play#116, rustore-onestore#10, rustore-onestore#11, samsung-amazon#37, samsung-amazon#96, huawei-xiaomi#87, aptoide-epic#36, google-play#24 |
| Korea permissions | tag: ONE Store, Samsung | For Korea, each permission is explained as essential or optional before it is asked. | rustore-onestore#68, samsung-amazon#39 |
| Advertising IDs | tag: Android, Ask AI | Ads and analytics use only the resettable advertising ID: Google's with the AD_ID permission, OAID on Huawei, or Amazon's after checking limit_ad_tracking. The opt-out is checked on every use, and the ID is never linked to IMEI, MAC, ANDROID_ID, App Set ID or personal data. | technical#79, google-play#114, google-play#51, google-play#52, google-play#53, technical#80, huawei-xiaomi#33, samsung-amazon#63, technical#81 |
| ATT | tag: Apple | The ATT prompt appears while the game is active, before any SDK reads the IDFA or tracks, and SDKs start in non-tracking mode. NSUserTrackingUsageDescription is specific, any pre-prompt screen is neutral, and the game works with tracking denied. No fingerprinting, and the IDFV is never combined for tracking. | apple#95, apple#96, apple#97, apple#99, apple#100, apple#107, technical#85, apple#40, apple#41 |
| Apple purpose strings | tag: Apple, Auto test | Every protected resource the game touches has a specific, non-empty Info.plist purpose string. | apple#101 |
| Privacy manifests | tag: Apple, Auto test | PrivacyInfo.xcprivacy declares the engine's required-reason APIs (UserDefaults CA92.1, FileTimestamp C617.1 and 0A2A.1, SystemBootTime 35F9.1, DiskSpace E174.1). Every listed SDK ships its own signed manifest, and native plug-ins have their own. | apple#103, apple#104, apple#105, apple#106, technical#86, technical#87, technical#88 |
| Ad network IDs | tag: Apple, Auto test | Info.plist lists every ad network's SKAdNetwork ID under SKAdNetworkItems. | technical#78 |
| Age signal APIs | tag: Apple, Samsung, Amazon | Where age laws apply, the build reads the store's age signal: Apple Declared Age Range (Xcode 26.2+, with parental approval for significant updates), Samsung Get Age Signals, Amazon GetUserAgeData with no test provider in production. | apple#108, apple#109, samsung-amazon#40, samsung-amazon#98, samsung-amazon#99 |
| No unprompted launches | main | Neither the game nor its SDKs open other apps, or start the game, without a player action. | huawei-xiaomi#35 |
| Minors' data | tag: Xiaomi | The game collects no data known to come from minors. | huawei-xiaomi#86 |
| Malware | drop: covered by A and J items | Code download, background work and permission items already cover these rejection reasons. | aptoide-epic#34 |
| Epic privacy | drop: Epic | - | aptoide-epic#46 |

## Web 2.0.0 mapping

Each item of `PublishingChecklistWebGL` 2.0.0 is filed under the same letter in Mobile 1.0.0.

- **keep:** the item carries over with mobile wording; it is a studio rule even where no store asks for it.
- **adapt:** the intent carries over, changed for native mobile.
- **reverse:** mobile requires the opposite (plan decision 15).
- **drop:** web-only or platform-only.

| Section | keep | adapt | reverse | drop |
| --- | --- | --- | --- | --- |
| A | A1, A2, A4, A5, A13, A14, A19 | A6 (200 MB initial download), A15 (no errors in logcat or the Xcode log), A17 (Android vitals memory) | - | A3, A7-A12, A16, A18, A20-A23 |
| B | B1-B6, B8-B18, B24 | B7 (no fill or offline instead of ad blockers), B19 (banners only on non-gameplay screens, inside the safe area, never over controls), B23 (only the build's approved ad networks) | - | B20-B22, B25, B26 |
| C | C1, C2, C4-C7, C13-C15 | C3 (price from store product data), C12 (the build's store billing only) | - | C8-C11 |
| D | D1-D5, D7, D13, D14, D16, D17 | D12 (cloud save where available, local fallback), D18 (a storage failure never crashes), D19 (account ID, never ANDROID_ID) | D6 (store, own or Apple login instead of platform-only) | D8-D11, D15, D20, D21 |
| E | E6 | - | E5 (third-party analytics allowed after consent) | E1-E4, E7-E9 |
| F | F2, F5, F6, F12, F13 | - | F21 (haptics allowed, with a Settings toggle) | F1, F3, F4, F7-F11, F14-F20, F22 |
| G | G1, G3, G5-G7, G9, G11-G16 | G2 (fill the screen at every aspect ratio), G4 (readable on the smallest supported phone; text at least 11 pt) | G21 (orientation set in Player Settings, not a console) | G8, G10, G17-G20, G22 |
| H | H1-H3, H5, H8-H10 | H6 (full Russian), H7 (system language, then English) | - | H4, H11 |
| I | I1-I4, I6, I7 | I5 (device mute and silent mode win) | - | I8 |
| J | J2-J6 | J1 (app lifecycle instead of tab visibility) | - | J7, J8 |
| K | K1-K4, K6, K7 | K5 (guests see a login button instead of leaderboards), K10 (store game services and review APIs) | - | K8, K9 |
| L | L1-L6 | L13 (TLS 1.2+ for every endpoint) | - | L7-L12, L14, L15 |
| M | M1-M8, M10-M13 | - | M9 (consent screen and UGC terms are required), M14 (privacy policy and own-store links are required), M15 (a support contact is required), M24 (own store only) | M16-M23 |
