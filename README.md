# Banked! iPhone test app

This folder turns the Banked! demo into a real iPhone app, so you can try it on your phone through TestFlight. The game itself is `www/index.html` (now the same file as `demos/banked-v11.html`). The `ios` folder is the Xcode project, already set up.

What the app adds over the web demo:
- Vibration works (the phone's own buzzes; web pages on iPhone can't vibrate).
- No browser bars, no status bar, no page bounce. Portrait only.
- The game stays clear of the notch and the home bar.
- Plain placeholder icon and launch screen (dark, blue square, green circle).

Nothing here has been built yet: this was set up on a computer without Xcode. The first build on a Mac may need a small fix.

## What you need

- A Mac with Xcode 27.1 (free from the Mac App Store).
- Node.js (free, from nodejs.org). It runs the setup commands.
- An Apple Developer account ($99 a year) for TestFlight. You can skip it for a quick test with a cable (step 4), but that copy stops working after 7 days.

## Steps

1. **Copy this folder to the Mac.** Leave out `node_modules` if it is there; step 2 makes it again.

2. **Set it up.** Open Terminal, go into the folder, and run:
   ```
   npm install
   npx cap sync ios
   npx cap open ios
   ```
   Xcode opens the project.

3. **Give it your name.** In Xcode, click **App** at the top of the left list, then the **Signing & Capabilities** tab.
   - **Team:** pick your Apple account.
   - **Bundle Identifier:** change `app.banked.game` to something only you use, such as `com.yourname.banked`. Put the same text in `capacitor.config.json` next to `appId`.

4. **Try it with a cable.** Plug in your iPhone, pick it at the top of Xcode, and press the ▶ button.
   - The first time, the iPhone asks you to turn on **Developer Mode** (Settings → Privacy & Security). Turn it on, let the phone restart, then press ▶ again.

5. **Send it to TestFlight.**
   - On appstoreconnect.apple.com: **Apps → + → New App**. Use the same Bundle Identifier and the name "Banked!" (or another if that's taken).
   - In Xcode: pick **Any iOS Device** at the top, then **Product → Archive**. When it finishes, click **Distribute App**, pick the TestFlight option, and follow the prompts to upload.
   - After 10 to 30 minutes it shows up under **TestFlight** in App Store Connect. Add yourself as a tester, then install the free TestFlight app on your iPhone to get it.

## Putting in a newer version of the game

1. Replace `www/index.html` with the new game file.
2. Run `npx cap sync ios`.
3. In Xcode, raise **Build** by one (App → General), then Archive and upload again (step 5).

## What to check on the phone

- Do the buzzes feel right? A light tap when the colour switches, a firmer one per kill, a strong one on the last kill, a "success" buzz when a wave is cleared. They can be turned off in Settings.
- Is a full pull comfortable with one thumb? (Settings → AIM changes the pull length.)
- Can you tell blue from green outdoors in bright light?
- Does it run smoothly, with no stutter during big chains?
- Close the app in the middle of a wave, open it again: CONTINUE should restart that wave with your cards.
- With the silent switch on, is the sound off? (Normal for games. Tell me if you'd rather keep sound on.)

## Files

- `www/index.html`: the game.
- `capacitor.config.json`: app name, id and background colour.
- `package.json`: the parts the app is built from (Capacitor 8.5 and its vibration plugin).
- `ios/`: the Xcode project. Already set to portrait only, no status bar, full screen on iPad, and "no special encryption" (so TestFlight skips that question).
