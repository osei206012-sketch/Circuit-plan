# Circuit Plan — native app project

This folder turns the Circuit Plan web app into a real iOS and Android app
using [Capacitor](https://capacitorjs.com), which wraps a web app in a thin
native shell. Everything up through "build and test on your own device" you
can do for free. Actually publishing requires your own developer accounts.

Run all of this on your own computer (not inside Claude) — you'll need
internet access and, for iOS, a Mac.

## 0. What you need

| | iOS | Android |
|---|---|---|
| Computer | Mac (required — Xcode only runs on macOS) | Windows, Mac, or Linux |
| Software | [Xcode](https://apps.apple.com/us/app/xcode/id497799835) (free, App Store) | [Android Studio](https://developer.android.com/studio) (free) |
| Developer account | [Apple Developer Program](https://developer.apple.com/programs/) — **$99/year** | [Google Play Console](https://play.google.com/console/signup) — **$25 one-time** |
| Also need | [Node.js](https://nodejs.org) (free) | Node.js (free) |

You can build and test the Android app without a Mac. For iOS you'll need
access to a Mac at least for the final build and submission step — a
borrowed one, a cloud Mac rental, or a friend's machine all work.

## 1. Install dependencies

In this folder:

```bash
npm install
```

## 2. Set your app ID

Open `capacitor.config.json` and change `"appId"` from
`com.yourname.circuitplan` to your own reverse-domain ID, e.g.
`com.janesmith.circuitplan`. Both app stores require this to be unique and
you can't easily change it later, so pick it now.

## 3. Add the native platforms

```bash
npx cap add ios
npx cap add android
```

This generates an `ios/` and `android/` folder — real native Xcode/Android
Studio projects — pointing at the `www/` folder as the app's content.

## 4. Generate app icons and splash screens

A starting icon and splash image are already in `resources/`. Generate all
the sizes both platforms need:

```bash
npx @capacitor/assets generate
```

Feel free to replace `resources/icon.png` (1024×1024) or
`resources/splash.png` (2732×2732) with your own art first, then re-run the
command above.

## 5. Sync and open

```bash
npx cap sync
npx cap open ios       # opens Xcode
npx cap open android   # opens Android Studio
```

From here it's a normal native app:

- **Test first** on a simulator/emulator or your own phone (plug it in, hit
  Run in Xcode or Android Studio).
- **iOS submission**: in Xcode, sign in with your Apple Developer account
  (Settings → Accounts), set your Team on the project, then
  Product → Archive, then use the Organizer window's "Distribute App" to
  upload to App Store Connect. From [appstoreconnect.apple.com](https://appstoreconnect.apple.com)
  you create the listing (name, screenshots, description, privacy policy
  URL) and submit for review (usually 1–3 days).
- **Android submission**: in Android Studio, Build → Generate Signed Bundle,
  create a signing key (keep it safe — you need the same one for every
  future update), then upload the resulting `.aab` file in the
  [Play Console](https://play.google.com/console) under your app's listing.
  Fill in the store listing and submit for review (often a few hours to a
  couple of days for a new app).

## 6. Keep editing the app

All the actual app code lives in `www/index.html` — it's the same file you've
been using. Edit it, then re-run `npx cap sync` and re-build in Xcode/Android
Studio to see changes. You don't need to re-add the platforms.

## About data & privacy

This app stores wiring plans only on the device, using local storage — it
never talks to a server. `PRIVACY.md` has a ready-to-use privacy policy; both
stores require you to host that text at a public URL and link it in your
listing.

## Suggested store listing copy

**Name:** Circuit Plan

**Subtitle / short description:** Pictorial electrical wiring planner

**Description:**
> Sketch an electrical wiring plan for any room or home. Drop in outlets,
> switches, lights, GFCIs, panels and more, wire them into circuits, and get
> a suggested breaker size and wire gauge for each one. Export your finished
> plan as an image to share or print.
>
> Circuit Plan is a planning tool, not a substitute for a licensed
> electrician — always have real electrical work reviewed and permitted by a
> professional.

**Category:** Utilities / Productivity (or Reference, Home & DIY where
available)

**Keywords:** electrical, wiring diagram, circuit planner, home DIY, outlet
layout, breaker panel, electrician, floor plan
