<p align="center">
  <img src="logo.png" alt="Near Health" width="96" height="96" style="border-radius: 24px;" />
</p>

<h1 align="center">Near Health — Landing Web</h1>

## What is this?

A lightweight landing page that acts as a **deep link gateway** for the Near Health mobile app. When a user receives an email containing a Near Health link and taps it, this page opens in their mobile browser and automatically redirects them into the app.

## How it works

```
Email link → Landing page (this project) → Near Health mobile app
```

1. **User taps a link in an email** — the link points to this hosted landing page and includes query parameters (e.g. policy activation data).
2. **The landing page attempts to open the app** — it uses the custom URL scheme `nearhealthapp://` to trigger a deep link, forwarding all query parameters from the URL.
3. **If the app is installed**, it opens directly to the correct screen (`onboarding/policy_activation`).
4. **If the app is not installed**, after a short delay the page shows download buttons for the App Store (iOS) and Google Play (Android).

## Deep linking strategy

The page uses two simultaneous strategies to maximize compatibility across mobile browsers:

- **Hidden iframe** — sets the `src` of a hidden iframe to the deep link URL (works on many iOS/Android browsers without a user gesture).
- **Window location fallback** — after 100ms, also sets `window.location.href` to the deep link as a backup.

On mobile devices, both strategies fire automatically on page load. On desktop, the user can tap the "Open Near Health" button manually.

## Configuration

| Setting | Value |
|---|---|
| Deep link scheme | `nearhealthapp://onboarding/policy_activation` |
| Fallback delay | 2 seconds |
| iOS App Store | `https://apps.apple.com/app/near-health/id000000000` |
| Google Play Store | `https://play.google.com/store/apps/details?id=com.nearhealth.app` |

## Project structure

```
├── index.html   # Landing page with deep linking logic
├── logo.png     # Near Health brand logo
└── README.md
```
