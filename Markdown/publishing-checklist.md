# Unity Mobile Publishing Checklist

> [!WARNING]
> **Check every store build yourself before you send it to us.** Every check that applies to your game and its stores must pass first. A build that fails comes back for fixes, and every round costs time on both sides, so please check carefully.

One checklist for Unity games on 9 mobile stores, listed in Sources: 8 Android stores and the Apple App Store. It covers the game builds. Store page material such as screenshots and descriptions is not covered.

1. The game has one codebase and one build per store. Each build contains only its own store's SDKs.
2. Main items pass in every store build.
3. Items that start with a store name apply only to that store's build. "Android" means all eight Android builds.
4. Blocks marked Optional cover features a game may not have. Skip the block if the game lacks the feature, otherwise every check in it is required.
5. Items under "Can be automated" are still required. Without tools or AI, check them by hand.
6. `Auto test` means a script can check the item and report pass or fail. `Ask AI` means an AI can review the code, text or assets.
7. Item numbers never change, so QA can report a failure briefly, like "G4 failed".

## A. Build & performance

- [ ] **A1.** A loading screen with progress shows at once. Heavy loading runs after the first screen, and no load lasts over 15 seconds without visible progress.
- [ ] **A2.** No splash or logo screens before the game, including Unity's if the license allows turning it off.
- [ ] **A3.** No crashes, freezes, force closes or ANRs in any flow: launch, tutorial, gameplay, ads, purchases, login, settings, rotation, rapid taps, and plugging in headphones or a charger.
- [ ] **A4.** Each store build is tested on a physical device from its store: iPhone and iPad, a Fire tablet, a Samsung Galaxy, a Xiaomi or Redmi, and a Huawei phone. Android builds are also tested with no SIM and no SD card.
- [ ] **A5.** The build is the final release: not a development build, and no placeholders, test data, debug menus, cheats, empty screens or buttons that do nothing.
- [ ] **A6.** Every server the game uses is live during review, and the game never needs an update before it can be played.
- [ ] **A7.** Gameplay averages 55-60 fps and never drops below 25 fps for long on the weakest target device.
- [ ] **A8.** Game speed and physics are the same at 60, 90 and 120 Hz.
- [ ] **A9.** No fast battery drain or overheating. Menus and idle screens cap the frame rate, and an hour of play starting at 33 C room temperature keeps the device under 40 C.
- [ ] **A10.** The first install is playable. Content needed before first play downloads only after the game shows its size and asks. Long downloads keep the screen awake, and a failed download shows a message and can retry.
- [ ] **A11.** Every online feature works on an IPv6-only network: ads, login, purchases, cloud saves and multiplayer. App Review tests on such networks.
  - Unity: connect by host name, never a hard-coded IPv4 address. Test with macOS Internet Sharing and "Create NAT64 Network".

**Can be automated**

- [ ] **A12.** `Auto test` The game is playable within 20 seconds of launch on the weakest target device (5 is the target).
- [ ] **A13.** `Auto test` The game starts and plays offline, and when any SDK fails to start.
- [ ] **A14.** `Auto test` No errors or exceptions in logcat or the Xcode console during a full play session.
- [ ] **A15.** `Auto test` Foreground memory stays under 2.25 GB on 4 GB RAM devices, and bitmap memory under 200 MB in the background.
- [ ] **A16.** `Auto test` Code shrinking is on when the build has over 50 MB of DEX code.
  - Unity: Player Settings > Publishing Settings > Minify > Release.
- [ ] **A17.** `Ask AI` The game never downloads or runs code, installs APKs, updates itself or adds home screen shortcuts, and it is not a web-view wrapper. Downloads are data and assets only, and updates come only from the store.
- [ ] **A18.** `Ask AI` No hidden or dormant features. Remote config may tune values, but never turns features on.
- [ ] **A19.** `Ask AI` The game calls only the SDK features it actually uses.
- [ ] **A20.** `Ask AI` **Apple:** Only public APIs and no deprecated frameworks. No SDK references UIWebView.

## B. Advertisement

**General**

- [ ] **B1.** No home-made ad units. Cross-promotion of your own games, if any, links only to the build's own store and shows no other store's name or badge.
- [ ] **B2.** The first ad shows only after the player has played.
- [ ] **B3.** Every ad is labeled as an ad, has a real, visible close button, and never imitates game UI, system dialogs or notifications. Full-screen ads that aren't rewarded can be closed within 15 seconds.
- [ ] **B4.** Ads show only inside the running game: never on the home or lock screen, in notifications or floating windows, or after the player leaves. No offerwalls.
- [ ] **B5.** The game never forces an ad click, never asks for personal data for ads, and never rewards clicking ads, installing other apps, rating or reviewing.
- [ ] **B6.** Input is blocked from the ad request until the ad closes. Gameplay and audio pause when the ad starts.
- [ ] **B7.** After an ad during play, the game resumes only when the player taps.
- [ ] **B8.** If an ad fails, has no fill or the device is offline, the game continues normally, with no penalty. Rewarded buttons with no ad behind them are hidden or disabled.
- [ ] **B9.** Progress is kept when the player taps an ad and comes back.
- [ ] **B10.** Players can see why an ad was shown and report an inappropriate ad without leaving the game, for example through the ad network's info button.
- [ ] **B11.** Promotional notifications go only to players who opted in inside the game, and Settings let them opt out.

**Interstitials**

- [ ] **B12.** Interstitials show only when the player continues into play after a break: Next level, Retry or Play.
- [ ] **B13.** Games without levels show them at natural moments, such as a death or round end, never on a timer.
- [ ] **B14.** Interstitials never show during active play, at the start of a level, before the loading screen, after every short action, when the player tries to leave, or from menu, settings, shop or inventory buttons.

**Rewarded ads** (Optional)

- [ ] **B15.** A rewarded ad starts only from a button with a video icon that names the exact reward. The button is never green.
- [ ] **B16.** The reward is a bonus. Every level can be finished without watching ads.
- [ ] **B17.** The reward is given only after the ad completes, never after an error or early close, and it is shown clearly.
- [ ] **B18.** One reward needs exactly one ad.
- [ ] **B19.** No rewarded buttons during active play. A continue option shows at the same time, at least as large, next to or above the reward button.
- [ ] **B20.** Rewarded offers are occasional: a revive at most once per attempt, and never right after an interstitial.
- [ ] **B21.** The same reward can also be earned without ads, for example with coins.

**Banners** (Optional)

- [ ] **B22.** Banners show only on screens without active gameplay, inside the safe area, and never cover buttons, text or controls.

**Platform-specific**

- [ ] **B23.** **Huawei:** Close buttons show from the start and never wait for a countdown, and closing an ad never opens another one.
- [ ] **B24.** **Huawei:** Ads open links only after a tap on their own click area, never on a shake or swipe, and never install apps by themselves.
- [ ] **B25.** **Huawei:** In Russia, Petal Ads uses SDK 4.60.301 or newer, ads are registered in ERIR, and an advertiser information button is shown.
- [ ] **B26.** **RuStore:** Ads come from networks that serve Russia, such as Yandex Mobile Ads or VK Ads. AdMob serves no users in Russia and no publishers based in Russia or Belarus.
- [ ] **B27.** **RuStore:** The game tells players it shows ads, the privacy policy lists the ad SDKs, the data they get and why, and every ad SDK is declared in the RuStore console.
- [ ] **B28.** **Xiaomi:** The AdMob app is registered with the store "Xiaomi GetApps", and app-ads.txt is set up.

**Can be automated**

- [ ] **B29.** `Ask AI` Ads come only from the ad networks approved for that store build.
- [ ] **B30.** `Ask AI` A cooldown in the game keeps interstitials at least 3 minutes apart. It is configurable per store.
- [ ] **B31.** `Ask AI` No invisible, hidden, stacked or auto-clicked ads, and the game is not built mainly to show ads.
- [ ] **B32.** `Ask AI` Every ad network and mediation adapter limits ad content to the 13+ rating or lower, with no gambling, adult or political ads.
- [ ] **B33.** `Auto test` **Huawei, Amazon:** Every ad network and adapter loads, shows and closes ads on a device without Google Play services. Builds use the full AdMob SDK, not Lite, and the Amazon build uses only Fire-compatible networks.

## C. In-app purchases (Optional)

- [ ] **C1.** The game is complete and balanced with purchases turned off. It charges nothing at first use and never locks main features behind payment.
- [ ] **C2.** Where purchases aren't available (country not supported, store app missing, outdated or signed out), every trace of them is hidden or the shop shows a clear message, and the game keeps working.
- [ ] **C3.** Each product shows the price from the store's product data in local currency, such as rubles on RuStore and won in Korea, and it matches the payment screen.
- [ ] **C4.** A product's image, name and contents match exactly what the player gets.
- [ ] **C5.** No paid random items: no loot boxes, gacha or random rewards bought with money or with a currency that can be bought.
- [ ] **C6.** The in-game product list matches the store console. Every product can be bought and is delivered in the submitted build, tested in that store's sandbox or test mode first.
- [ ] **C7.** Shop offers don't pop up before the player has played.
- [ ] **C8.** A failed, cancelled or pending purchase grants nothing and leaves the game working. A pending purchase tells the player that payment is still waiting.
- [ ] **C9.** Settings have a Restore Purchases button for non-consumables and subscriptions.
- [ ] **C10.** Subscriptions, if any, last at least 7 days, keep giving value, and show price, period, auto-renewal and how to cancel before purchase.

**Platform-specific**

- [ ] **C11.** **Huawei:** Subscriptions never auto-renew by default, and the purchase page shows the renewal terms and how to cancel.
- [ ] **C12.** **Xiaomi:** GetApps purchases run from an enterprise developer account with payment details set up.
- [ ] **C13.** **RuStore:** Every payment method is declared in the console, two-step payments are confirmed within 6 hours, and payment works without RuStore installed.
- [ ] **C14.** **ONE Store:** The game asks the player to update or sign in to ONE store when billing requests it. The global build sells no subscriptions, and in Korea every item that can't be cancelled says so before purchase.
- [ ] **C15.** **Amazon:** Purchases are tested on the 64-bit (ARM64) Fire build, because Amazon's Unity plugin 3.0.2 contains 32-bit libraries only.
  - Unity: for ARM64, use Appstore SDK 3.0.8 or newer through your own Java or Kotlin bridge.

**Can be automated**

- [ ] **C16.** `Ask AI` Each store build sells digital items only through its own store's billing: Google Play Billing, StoreKit, HUAWEI IAP, Samsung IAP, Xiaomi GetApps IAP, RuStore Pay SDK, ONE store IAP, Amazon Appstore SDK or Aptoide Billing SDK. No links, buttons or text lead to another payment method. Bought currency never expires and is spent only in this game.
- [ ] **C17.** `Auto test` Purchases completed while the game was closed, or outside it, are delivered at launch and on return to the game.
- [ ] **C18.** `Auto test` Each purchase is granted exactly once, even if the restore runs again.
- [ ] **C19.** `Auto test` Every purchase is verified, on a server where the store offers it, then consumed or acknowledged at once, within 48 hours at most.
- [ ] **C20.** `Ask AI` A purchase is saved right away, to the cloud where available.
- [ ] **C21.** `Auto test` **Google Play:** Play Billing Library 8 or newer, with its version meta-data kept in the merged manifest. Move to version 9 before 31 August 2027.
  - Unity: Unity IAP 4.14.0+ or 5.0.0+; 5.4.0+ for Play Billing Library 9.
- [ ] **C22.** `Ask AI` **Apple:** Purchases use StoreKit 2. AppStore.sync runs only after a tap on Restore Purchases, and receipt checks accept the SHA-256 certificate.
  - Unity: Unity IAP 5.
- [ ] **C23.** `Ask AI` **Huawei:** Purchases use HUAWEI IAP.
- [ ] **C24.** `Auto test` **Samsung:** Samsung IAP 6 runs in production mode, no Samsung IAP 4 permission or library is left, and GetOwnedList runs at every launch.
  - Unity: Samsung IAP Unity plugin 6.5.2.
- [ ] **C25.** `Auto test` **Xiaomi:** GetApps IAP SDK 1.1.8 or newer, and every purchase passes a stable, unique obfuscatedAccountId of at most 200 characters.
- [ ] **C26.** `Auto test` **RuStore:** Purchases use RuStore Pay SDK, not the retired BillingClient SDK.
  - Unity: Activity is UnityPlayerActivity (GameActivity breaks payments), Minimum API Level is 24, and PayClientSettings has the console app ID and a unique deeplink scheme.
- [ ] **C27.** `Auto test` **ONE Store:** ONE store IAP SDK 21.04.00, and server checks outside Korea send the x-market-code header.
- [ ] **C28.** `Ask AI` **Amazon:** Purchases use Amazon Appstore SDK 3.0.9, not Unity IAP 5 and not the unsupported Billing Compatibility SDK.
- [ ] **C29.** `Ask AI` **Aptoide:** The Aptoide Billing SDK replaces Play Billing, starts with the console public key, and completes purchases without the Aptoide Wallet app.
  - Unity: Aptoide Unity billing plugin, with its Android files only once in Assets/Plugins/Android.

## D. User data

**Saves and personal data**

- [ ] **D1.** Progress saves right after each meaningful action: level done, unlock, purchase.
- [ ] **D2.** Progress, purchases, settings and sign-in survive a restart, an update and backgrounding.
- [ ] **D3.** Progress can be restored after a reinstall or on a new device, through cloud saves or login.
- [ ] **D4.** No personal data fields: age, email, location. Name input is allowed only with a profanity filter.

**Login** (Optional)

- [ ] **D5.** Guest play is the default, and no login is needed to start or play.
- [ ] **D6.** Login opens only when the player presses a button, with a short reason why.
- [ ] **D7.** Login never depends on a single third-party provider: the store's account or the game's own account also works. Account creation and sign-in work in every store build.
- [ ] **D8.** Guest progress carries over at login, and synced progress follows the player across devices.
- [ ] **D9.** Settings have a Delete account option. It deletes the account and its personal data within 15 working days, without contacting support, and says what is kept and for how long. Deactivation alone does not count.
- [ ] **D10.** A web page lets players request account deletion without the game. Its URL goes into the hand-off list (N8).

**Platform-specific**

- [ ] **D11.** **Apple:** Any third-party login comes with Sign in with Apple. Social logins can be revoked in the game, social tokens never leave the device, and Sign in with Apple relay addresses on both domains are accepted.
- [ ] **D12.** **Huawei, Amazon:** Login works without Google Play services, with no Google Sign-In.
- [ ] **D13.** **RuStore:** Personal data of players in Russia, such as accounts, cloud saves and analytics profiles, is stored on servers in Russia. The law (152-FZ) covers Russian players in every build, and RuStore checks it.

**Can be automated**

- [ ] **D14.** `Ask AI` All saves go through one save layer: cloud saves where the build has them, local storage otherwise.
  - Unity: one save interface with a backend per store.
- [ ] **D15.** `Ask AI` The game loads saved data before play starts or anything is saved.
- [ ] **D16.** `Auto test` Saves are batched to at most one every 3 seconds.
- [ ] **D17.** `Auto test` Saves from older versions load without errors.
- [ ] **D18.** `Auto test` A missing or broken save starts a fresh game instead of crashing.
- [ ] **D19.** `Auto test` A storage failure, such as a full disk, never crashes the game.
- [ ] **D20.** `Ask AI` Players are identified by an account ID, never by ANDROID_ID, username or local data. ANDROID_ID differs between builds signed with different keys.
- [ ] **D21.** `Ask AI` **Google Play, Apple:** Play Games Services and Game Center player IDs are never the main account identity, and Game Center IDs are never shown or shared.

## E. Analytics & events

- [ ] **E1.** Analytics collects data only with the player's consent (O2), uses it only for the purpose consented to, and stops when the player withdraws consent in Settings. Personal data reaches third parties, AI services included, only with explicit permission.

**Can be automated**

- [ ] **E2.** `Auto test` A missing or failing analytics SDK never blocks or crashes the game.
- [ ] **E3.** `Auto test` **Huawei, Amazon:** Analytics and crash reporting work without Google Play services: only Firebase libraries that need no Play services, or SDKs tested on a Fire tablet.

## F. Controls

- [ ] **F1.** The whole game is playable with touch only.
- [ ] **F2.** Hints match touch devices: no key names, mouse icons or "click" texts.
- [ ] **F3.** Controls are explained in the game before or during the first play.
- [ ] **F4.** Touch targets are at least 7 mm (44 pt), their hit areas match their graphics, and buttons are spaced so taps don't land on the wrong one.
- [ ] **F5.** Tapping a text field opens the on-screen keyboard, and the field stays visible above it.
- [ ] **F6.** No input lag, and no ignored input.
- [ ] **F7.** The game never changes system settings or standard buttons: volume buttons, the silent switch, Bluetooth, GPS or restarts.
- [ ] **F8.** Vibration, if used, is short, follows game events, and can be turned off in Settings.

**Platform-specific**

- [ ] **F9.** **Android:** The Back gesture and button close the top popup, pause gameplay, or ask to exit on the main screen. They never force-close the game, and no screen traps the player.
  - Unity: turn on Predictive Back Gesture Support. With target API 36, Android 16 no longer sends the old Back event.

## G. User interface

- [ ] **G1.** The game fills the whole screen on every phone and tablet aspect ratio, without stretching.
- [ ] **G2.** The game draws edge to edge, and HUD, buttons and banners stay inside the safe area: notch, Dynamic Island, cutouts, status and navigation bars, home indicator.
  - Unity: use Screen.safeArea. "Render outside safe area" has no effect on Android 15 and newer.
- [ ] **G3.** Rotation, folding, split screen and window resizing re-lay out the UI without stretching, clipping or lost state, and the game follows the device's orientation lock.
- [ ] **G4.** Text and icons are readable on the smallest supported phone, with text at least 11 pt, and sharp on high-density screens.
- [ ] **G5.** Every popup has a visible close button.
- [ ] **G6.** Icons are drawn, not emoji, and universal: gear for settings, speaker for sound, globe for language.
- [ ] **G7.** No exit or quit button.
- [ ] **G8.** Every visible button works. No placeholders, debug UI, FPS counters or test buttons.
- [ ] **G9.** New players reach gameplay with one tap at most.
- [ ] **G10.** Complex mechanics get a short, visual tutorial at the start that players can skip.
- [ ] **G11.** Cutscenes and intros can be skipped.
- [ ] **G12.** The game tells the player clearly when all content is finished.
- [ ] **G13.** The installed name and icon match the store listing. There is exactly one launcher icon, it does not look like a system icon, and there are no fake badges.
- [ ] **G14.** Settings show a support contact, such as an email address or a page.

**Platform-specific**

- [ ] **G15.** **Apple:** The iPhone game also runs on iPad, declares all four orientations on iPad, doesn't rely on UIRequiresFullScreen, and is tested on iPhone Duo.
- [ ] **G16.** **ONE Store:** Orientation stays locked while the ONE store purchase screen is open.

**Can be automated**

- [ ] **G17.** `Ask AI` Orientation is set in Player Settings, and code never switches it during play.
- [ ] **G18.** `Auto test` **Android:** The merged manifest declares android:appCategory="game", so Android 16 keeps the game's orientation on tablets and foldables.
  - Unity: Player Settings > Other Settings > App Category: Game.
- [ ] **G19.** `Auto test` **Apple:** Info.plist has a launch screen key. Uploads built with the iOS 27 SDK fail without one (ITMS-90870).

## H. Localization

- [ ] **H1.** The game starts in the device language, with no language picker before play.
- [ ] **H2.** A manual language switch, if present, uses a globe icon and shows each language by its own name (English, Русский).
- [ ] **H3.** Text fits its space in every language. Russian runs about 30% longer than English.

**Can be automated**

- [ ] **H4.** `Ask AI` English is included and is the default and fallback language.
- [ ] **H5.** `Ask AI` Russian is included in full, for every text players see, and used for players set to ru, be, kk, uk or uz. Russian law (168-FZ) has required it since 1 March 2026.
- [ ] **H6.** `Ask AI` The language comes from the device, then English.
- [ ] **H7.** `Ask AI` Every text in the game is translated, down to small labels and tooltips. Only decorative text that isn't needed to play, like graffiti or signs, may stay as it is.
- [ ] **H8.** `Ask AI` Spelling and grammar are correct, and there is no profanity in any language.
- [ ] **H9.** `Auto test` Fonts contain every character of every supported language.
  - Unity: TextMeshPro atlases include Cyrillic, or use a fallback font.
- [ ] **H10.** `Ask AI` **Apple:** Every Info.plist purpose string is translated into each supported language.
- [ ] **H11.** `Ask AI` **Android:** Language detection accepts the codes he, yi and id, which API 35 no longer converts to iw, ji and in.

## I. Audio

- [ ] **I1.** The game has music, sound effects and UI sounds.
- [ ] **I2.** Settings have separate music and sound effect toggles, and there is no "mute all" button.
- [ ] **I3.** Sound settings are saved and restored.
- [ ] **I4.** All audio stops whenever the game pauses (see J).
- [ ] **I5.** The device's mute switch or silent mode silences the game, and the device volume always wins.
- [ ] **I6.** Volume is consistent, with no sudden loud sounds.
- [ ] **I7.** Audio stops for calls, sleep and backgrounding, and comes back correctly afterwards.

**Platform-specific**

- [ ] **I8.** **Apple:** The audio session uses the Ambient or Solo Ambient category, never Playback, and Info.plist declares no background modes the game doesn't use.
- [ ] **I9.** **Android:** Audio focus is requested only in the foreground and released when another app plays audio.

## J. Pause

- [ ] **J1.** Leaving the game (Home, a call, a notification, the app switcher, settings or an external link) pauses it and saves state. Returning restores it with no lost progress.
- [ ] **J2.** A pause button is available during gameplay.
- [ ] **J3.** After any automatic pause during play, the game shows a pause screen and resumes on the player's input.
- [ ] **J4.** The game works fully with notifications denied.
- [ ] **J5.** No in-game update or reboot prompts. Updates come only from the store.

**Can be automated**

- [ ] **J6.** `Ask AI` One pause switch controls the whole game: gameplay, physics, timers, audio and input.
  - Unity: one controller owns `Time.timeScale` and `AudioListener.pause`, and nothing else writes them.
- [ ] **J7.** `Auto test` Pause reasons stack, so the game resumes only after all of them end.
- [ ] **J8.** `Auto test` Progress saves when the game goes to the background.
- [ ] **J9.** `Ask AI` No foreground services, full-screen intents, exact alarms, floating windows, auto-start, lock screen or launcher changes, blocking of other apps' ads, or bypassing of power management.

## K. Social interactions (Optional)

- [ ] **K1.** Where a feature isn't available, its button and every mention of it are hidden.
- [ ] **K2.** Share, rate and invite prompts never interrupt gameplay and show at most once per session.
- [ ] **K3.** Store dialogs for purchases, invites and sharing open only after a player action.
- [ ] **K4.** No feature is locked behind sharing, inviting friends or rating, and the game never rewards a rating or review.
- [ ] **K5.** The rating prompt is the store's own review dialog, shown after a success such as a finished level. It never appears on first launch, mid-level or right after a button tap, and no "Do you like the game?" question comes first. A "Rate us" button opens the store page instead.
- [ ] **K6.** "Rate us", "More games" and cross-promotion links open the store the build is for, never another store.
- [ ] **K7.** Sharing sends nothing until the player confirms the content and recipients. It shares only game images or text, with no QR codes or download links, and shows a message when the needed app is missing.
- [ ] **K8.** Guests see a login button in place of leaderboards, never an error.
- [ ] **K9.** The best score sent to a leaderboard matches the best score in the save.
- [ ] **K10.** Leaderboards show store or account names. Names typed in the game pass a profanity filter.

**Can be automated**

- [ ] **K11.** `Ask AI` Each build uses its own store's review API: Play In-App Review, StoreKit requestReview, AppGallery in-app comments, Galaxy Store Review Broadcast, or the RuStore Review SDK at most once a day. The Xiaomi, ONE Store, Amazon and Aptoide builds only open their store page.
- [ ] **K12.** `Auto test` **Apple:** If the game uses Game Center, the build has the Game Center entitlement and its features are set up in App Store Connect.
- [ ] **K13.** `Ask AI` **Google Play:** Play Games Services, if used, is the v2 SDK and signs in automatically at launch, and play continues if sign-in fails.
- [ ] **K14.** `Ask AI` **Huawei, Amazon:** Leaderboards, achievements and cloud saves use the game's own backend or one that works without Google services, never Play Games Services.

## L. Multiplayer (Optional)

- [ ] **L1.** A match starts within seconds even when nobody is online, thanks to bots or a solo mode.
- [ ] **L2.** Solo play is as easy to find as multiplayer.
- [ ] **L3.** Players see store or account usernames, and any names they type pass a profanity filter.
- [ ] **L4.** Chat, names, avatars and other player content follow rules players accept first, with filtering, in-game reporting of content and players, blocking and a published moderation contact. Chat can be turned off in Settings, and chat with strangers is never the main feature.
- [ ] **L5.** A lost connection shows a message with a reconnect option, and the game never freezes.
- [ ] **L6.** In online matches, a pause only stops this player's audio and input. The match goes on, and the player gets a pause screen on return.
- [ ] **L7.** Voice chat, camera and gameplay recording ask for consent first and show an indicator while recording.

**Platform-specific**

- [ ] **L8.** **Amazon:** Chat and other player content sit behind an age check.
- [ ] **L9.** **RuStore:** If chat makes the studio an information distribution organizer (149-FZ), the studio is registered with Roskomnadzor and stores chat data as 374-FZ requires.
- [ ] **L10.** **ONE Store:** In Korea, chat shows caution and sanction notices and warns players not to share bank, ID or card numbers.

**Can be automated**

- [ ] **L11.** `Auto test` Every server the game talks to uses TLS 1.2 or newer (HTTPS and WSS), and personal data never travels unencrypted.
- [ ] **L12.** `Auto test` **Android:** LAN multiplayer, if any, declares NEARBY_WIFI_DEVICES and works with the local network restriction turned on.

## M. Content & links

**Content**

- [ ] **M1.** Content is family-friendly and suits all ages, but the game isn't made or labeled for children: no "for kids" wording, and no imagery or characters that make it look made for kids.
- [ ] **M2.** No graphic violence or blood, sustained horror, or realistic violence toward animals, children or the elderly.
- [ ] **M3.** No politics, war, religion, black magic, fortune telling, gambling or cheating.
- [ ] **M4.** No drugs, alcohol, tobacco, sexual content, profanity, hate, self-harm or discrimination.
- [ ] **M5.** No real or photorealistic people: no photos, video or face scans, AI-generated included.
- [ ] **M6.** No interactive AI in the game. Assets generated with AI in advance are fine, with no watermarks or leftover prompt text.
- [ ] **M7.** No AI-made imitations of real places or events.
- [ ] **M8.** No real money, prizes, promo codes or tradable items. Rewards have value only inside the game, and contests, if any, are run by the studio with in-game rules saying the store isn't involved.
- [ ] **M9.** Content keeps the game at 13+ or lower in every store: no simulated gambling such as slots or casino games (M3), no free web browser, and no paid random items (C5).
- [ ] **M10.** Updates keep the same game. A different game is a new submission.
- [ ] **M11.** Each game is a distinct product with real, lasting gameplay, not a reskin or near-copy of another studio game in the same store.
- [ ] **M12.** Where a law requires age checks (US states with app store age laws, Brazil, Korea), the game reads the store's age signal and restricts the affected features.

**Copyright**

- [ ] **M13.** All code, art, music, sounds, fonts and names are original or licensed, with proof ready on request. No clones, reskins or barely changed templates.
- [ ] **M14.** No well-known names, trademarks or celebrities in the title or the game, and nothing implies a link to the store or a device maker.
- [ ] **M15.** No characters, models, textures or sounds copied from or imitating a known game, film or brand, such as Roblox avatars or Minecraft blocks and mobs.

**Links and branding**

- [ ] **M16.** Outgoing links go only to the privacy policy, the account deletion page, the support contact and the build's own store. No other websites, social media, surveys or QR codes.
- [ ] **M17.** The game offers no downloads of other apps, has no app store features, and never pushes players to install or open another app.
- [ ] **M18.** No extra user agreements or terms popups beyond the consent screen (O2) and, with player content, its rules (L4).

**Platform-specific**

- [ ] **M19.** **RuStore:** No justification of extremism or Nazism, LGBT "propaganda" (398-FZ), discrediting of the Russian army or state symbols, drugs as a game mechanic, new depictions of alcohol or tobacco use, or mockery of real tragedies.

**Can be automated**

- [ ] **M20.** `Ask AI` The game names only its own store and platform: no other store's, platform's or device brand's name, logo or badge, such as "Google Play" or "Android" in the iOS build.
- [ ] **M21.** `Ask AI` The game never asks players to turn off Play Protect or other device security.

## N. Store builds

- [ ] **N1.** Every store build is released together at the same version, so no store falls behind.
- [ ] **N2.** All Android builds share one final package name, which matches each store console and never changes.
- [ ] **N3.** All Android builds are signed with the same app signing key, held by your studio, because Aptoide requires the Google Play signature for games with purchases. Google Play App Signing uses your uploaded key, not one Google generates. Samsung, Huawei and ONE Store get the same key for their signing, or the build is an APK you sign.
- [ ] **N4.** Every package name and every signing certificate used by any store build, including the certificates of stores that re-sign, is registered for Android developer verification, and every keystore is backed up. Unregistered apps can't be installed from Google Play, Samsung or Xiaomi in Brazil, Indonesia, Singapore and Thailand since 30 September 2026, and from any store worldwide in 2027.
- [ ] **N5.** Google Play's automatic installer check is off in Play Console, and no build gates play on Play Integrity, so installs from other stores are never blocked.
- [ ] **N6.** QA installs each store build over every other store's build. The result matches the signing plan, and on Android 14 or newer an update from a second store asks for approval and keeps the save.
- [ ] **N7.** Phones and tablets only: Google Play Games on PC, Apple silicon Mac and Apple Vision Pro availability are turned off, and unsupported devices are excluded in each console, not in code.
- [ ] **N8.** Each store build comes with a hand-off list for the store forms: every SDK with its version, the permissions, the data collected or shared and why, Advertising ID use, ads, purchases, chat, data sent abroad, and the privacy policy and account deletion URLs.

**Platform-specific**

- [ ] **N9.** **Amazon:** The Fire build targets Fire tablets only. Alexa tablets get the Google Play build.
- [ ] **N10.** **Amazon:** Login keys, anti-tamper checks and SDK key hashes use the certificate hashes Amazon shows in the Developer Console, because Amazon re-signs the app.
- [ ] **N11.** **Samsung:** Vietnam is excluded from the distribution countries.
- [ ] **N12.** **Xiaomi:** For a game not on Google Play, the console's verification APK keeps its name and package, is signed with the game's key using v2 or v3, and is at most 4 MB. "Auto update" from Google Play is off.

**Can be automated**

- [ ] **N13.** `Auto test` The project uses Unity 6000.0.68f1 or newer, or 6000.3.8f1 or newer. Unity 2022.3 can't meet the 16 KB, Yandex Ads and iOS 27 requirements.
- [ ] **N14.** `Auto test` Each store build contains only its own store's SDKs for billing, login, reviews, updates, push and game services. No HMS libraries outside the Huawei build, and no other store's SDK in the Google Play build.
- [ ] **N15.** `Auto test` **Huawei, Amazon:** The full core loop (play, saves, purchases, ads) works on a device without Google Play services, and no SDK needs them: no Play Billing, Google Sign-In, Play Games Services, Firebase Cloud Messaging, Play Integrity, or Play review and update APIs. Push uses HMS Push or Amazon Device Messaging.
- [ ] **N16.** `Auto test` **Android:** Every Android build targets API level 36.
  - Unity: Player Settings > Other Settings > Target API Level 36.
- [ ] **N17.** `Auto test` **Android:** minSdkVersion is 24 to 28, and compileSdk is 35 or higher.
  - Unity: Unity 6000.3 allows 25 as the lowest Minimum API Level.
- [ ] **N18.** `Auto test` **Android:** Every build ships arm64-v8a and armeabi-v7a, because some Fire tablets are 32-bit only.
  - Unity: IL2CPP with Target Architectures ARMv7 and ARM64.
- [ ] **N19.** `Auto test` **Android:** Every native library is 16 KB aligned, `zipalign -c -P 16 -v 4` passes, and the game runs on a 16 KB device or emulator without the compatibility warning. Google Play blocks updates without it from 1 February 2027.
  - Unity: 6000.0.45f1 or newer, and Burst 1.8.21 or newer.
- [ ] **N20.** `Auto test` **Android:** The release is not debuggable, uses APK Signature Scheme v2 and v1, declares android:exported on every component with an intent filter, uses no code packers, and has a versionName under 50 characters.
- [ ] **N21.** `Auto test` **Android:** versionCode goes up with every release, is never reused and stays at or below 2100000000. Every non-Play build's code is higher than the Play build's, for example with a store digit in front.
- [ ] **N22.** `Auto test` **Android:** No SDK version that Google's SDK Index marks as policy-violating, or as outdated for more than 90 days.
- [ ] **N23.** `Auto test` **Google Play:** The upload is an AAB with no OBB files. Large content uses Play Asset Delivery within its limits: 500 MB base module, 1.5 GB per asset pack, 4 GB install-time total.
- [ ] **N24.** `Auto test` **Huawei, Samsung, Xiaomi, RuStore, ONE Store, Amazon, Aptoide:** The build is one universal APK of 2 GB or less, with no OBB files and no fast-follow or on-demand asset packs. Anything larger downloads in the game.
  - Unity: Build App Bundle off, Split Application Binary off.
- [ ] **N25.** `Auto test` The initial download is 200 MB or less, the size at which Google Play and iOS start asking before downloading over mobile data.
- [ ] **N26.** `Auto test` **ONE Store:** The manifest has the ONE store queries, the release has no dev_option meta-data or SDK log level calls, and the global build is one binary signed through ONE store app signing with your studio key.
- [ ] **N27.** `Auto test` **Amazon:** Hardware features implied by permissions are marked android:required="false", there are no wallpaper, widget or lock screen features, and hardware acceleration is on.
- [ ] **N28.** `Auto test` **Apple:** The build uses Xcode 26 or newer and the iOS 26 SDK, moving to Xcode 27 and the iOS 27 SDK from April 2027. It supports the UIScene life cycle, and native plug-in callbacks are tested after the UIScene switch.
  - Unity: 6000.0.68f1 or newer, or 6000.3.8f1 or newer.
- [ ] **N29.** `Auto test` **Apple:** The deployment target is iOS 15 or later, and UIRequiredDeviceCapabilities lists only what the game can't run without.
- [ ] **N30.** `Auto test` **Apple:** The app is 4 GB or less uncompressed, with at most 500 MB of executable code (__TEXT). It has no On-Demand Resources and no bitcode, sets ITSAppUsesNonExemptEncryption, and uploads with a matching bundle ID and a new build number.

## O. Privacy & permissions

- [ ] **O1.** Settings and the first-run consent screen link the privacy policy, in English and Russian, at the same URL given to every store. It lists the data collected, why, every SDK that receives data, retention, deletion, how to withdraw consent, and a contact.
- [ ] **O2.** On first launch, before any SDK collects personal data, a consent screen says what is collected and why. Agree and Reject buttons are equally prominent, and nothing is pre-checked. Consent is separate from any terms, and Settings can change it.
- [ ] **O3.** Settings have a switch that turns personalized ads off.
- [ ] **O4.** No permission is requested at first launch. Each one is asked when its feature is used, with its purpose shown, and a denial never blocks play or sign-in or causes repeated prompts.
- [ ] **O5.** No feature, reward or content depends on allowing tracking, notifications, location or other permissions.
- [ ] **O6.** Neither the game nor its SDKs open other apps, or start the game, without a player action.

**Platform-specific**

- [ ] **O7.** **Apple:** The tracking (ATT) prompt appears while the game is active, before any SDK reads the IDFA or tracks, and SDKs start in non-tracking mode. Any screen before it is neutral, and the game works with tracking denied.
- [ ] **O8.** **Apple, Samsung, Amazon:** Where age laws apply, the build reads the store's age signal: Apple Declared Age Range (Xcode 26.2 or newer), Samsung Get Age Signals, or Amazon GetUserAgeData, with no test provider in production.
- [ ] **O9.** **ONE Store, Samsung:** For Korea, each permission is explained as essential or optional before it is asked.
- [ ] **O10.** **Xiaomi:** The game collects no data known to come from minors.

**Can be automated**

- [ ] **O11.** `Auto test` Builds with AdMob show a Google-certified consent tool (IAB TCF v2.3 with disclosedVendors) before personalized ads in the EEA, the UK and Switzerland, and send US state privacy signals (GPP or RDP).
- [ ] **O12.** `Auto test` **Android:** The merged manifest, SDK additions included, holds only permissions a feature needs. None of these: QUERY_ALL_PACKAGES, MANAGE_EXTERNAL_STORAGE, broad photo, video or contacts access, READ_LOGS, SYSTEM_ALERT_WINDOW, phone or SMS, accessibility or device admin, REQUEST_INSTALL_PACKAGES, or location for ads or analytics.
- [ ] **O13.** `Ask AI` **Android:** Ads and analytics use only the resettable advertising ID: Google's with the AD_ID permission, OAID on Huawei, or Amazon's after checking limit_ad_tracking. The opt-out is checked on every use, and the ID is never linked to IMEI, MAC, ANDROID_ID, App Set ID or personal data.
- [ ] **O14.** `Ask AI` **Apple:** No fingerprinting, the IDFV is never combined with other data for tracking, and NSUserTrackingUsageDescription is short and specific.
- [ ] **O15.** `Auto test` **Apple:** Every protected resource the game touches has a specific, non-empty Info.plist purpose string.
- [ ] **O16.** `Auto test` **Apple:** PrivacyInfo.xcprivacy declares the engine's required-reason APIs: UserDefaults CA92.1, FileTimestamp C617.1 and 0A2A.1, SystemBootTime 35F9.1, DiskSpace E174.1. Every SDK on Apple's list ships its own signed manifest, and native plug-ins have their own.
- [ ] **O17.** `Auto test` **Apple:** Info.plist lists every ad network's SKAdNetwork ID.

## Sources

Checked on 17 November 2026, together with Mirra Games publishing experience. Sources marked "partial" publish only part of their rules. Epic Games Store was researched but left out, because its mobile developer rules are not public yet. The full research, with a source for every rule, is in `Documentation/Research`.

1. [Google Play Developer Program Policy](https://support.google.com/googleplay/android-developer/answer/16933379)
2. [Google Play target API level requirements](https://support.google.com/googleplay/android-developer/answer/11926878)
3. [Google Play app size limits](https://support.google.com/googleplay/android-developer/answer/9859372)
4. [Google Play Billing Library deprecation](https://developer.android.com/google/play/billing/deprecation-faq)
5. [Android: support 16 KB page sizes](https://developer.android.com/guide/practices/page-sizes)
6. [Android developer verification](https://developer.android.com/developer-verification)
7. [Apple App Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
8. [Apple upcoming requirements](https://developer.apple.com/news/upcoming-requirements/)
9. [Apple maximum build file sizes](https://developer.apple.com/help/app-store-connect/reference/app-uploads/maximum-build-file-sizes)
10. [AppGallery Review Guidelines, partial](https://developer.huawei.com/consumer/en/doc/app/50104-overview)
11. [Galaxy Store App Distribution Guide, partial](https://developer.samsung.com/galaxy-store/distribution-guide.html)
12. [Galaxy Store FAQ](https://developer.samsung.com/galaxy-store/faq.html)
13. [Xiaomi GetApps Review Guidelines, partial](https://global.developer.mi.com/document?doc=appReview.reviewGuidelines)
14. [RuStore app requirements](https://www.rustore.ru/help/developers/publishing-and-verifying-apps/requirement-apps)
15. [RuStore signing keys](https://www.rustore.ru/help/developers/publishing-and-verifying-apps/app-publication/apk-signature)
16. [ONE store Review Guidelines](https://onestore-dev.gitbook.io/dev/eng/docs/review/one-store-review-guideline)
17. [Amazon Appstore test criteria](https://developer.amazon.com/docs/app-testing/test-criteria.html)
18. [Amazon Fire OS device filtering](https://developer.amazon.com/docs/app-submission/device-filtering-and-compatibility.html)
19. [Aptoide Connect app files](https://docs.connect.aptoide.com/docs/app-files)
20. [Aptoide PSV formula](https://docs.connect.aptoide.com/docs/psv)
21. [Unity: 16 KB page size support](https://discussions.unity.com/t/info-unity-engine-support-for-16-kb-memory-page-sizes-android-15/1589588)
22. [Unity: UIScene life cycle support](https://discussions.unity.com/t/info-apple-update-your-editor-to-receive-uiscene-lifecycle-support/1709065)
