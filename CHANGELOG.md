# Unity Mobile Publishing Checklist 1.0.0

### What's new

1. One checklist for 9 mobile stores: Google Play, Apple App Store, Huawei AppGallery, Samsung Galaxy Store, Xiaomi GetApps, RuStore, ONE Store, Amazon Appstore and Aptoide
2. 257 checks in 15 sections, in English and Russian, 88 of them marked `Auto test` or `Ask AI`
3. Rules for per-store builds: one codebase, each build with only its own store's SDKs, one Android signing key, and version codes that keep the store builds apart
4. Unity 6000.0.68f1 or 6000.3.8f1 is the minimum, for 16 KB memory pages, target API 36 and the iOS 27 SDK
5. Research on every store with a source for each rule, and a matrix that maps every rule to a check or a recorded reason to drop it
6. Print-ready PDFs of both languages from one command

### Known issues

1. Epic Games Store is planned for a later version, because its rules for mobile developers are not public yet
2. Samsung's Seller Portal guides, and Huawei's 64-bit and target API rules, could be checked only in part
3. Unity has published no minimum version for Xcode 26. The minimum above is expected to cover it, but no Xcode 26 build has been made to confirm it
