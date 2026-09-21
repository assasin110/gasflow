# Orifice Gas Flow Calculator

A free, offline-capable web app for checking flow through an orifice meter and sizing orifice plates for a meter run. Built on the AGA 3 and AGA 8 standards used across the natural gas industry.

Installs to a phone's home screen like a native app — no App Store, no account, no data leaving the device.

## What it does

**Check flow** — enter a meter's pipe size, orifice bore, differential pressure, static pressure, and gas composition, and get the flow rate at base conditions, along with the full set of intermediate values (Reynolds number, expansion factor, discharge coefficient, compressibility, and more).

**Size orifice** — enter a pipe size, target flow range, and maximum differential, and the app works backward to the exact bore that fits, then lists the nearest standard plate sizes (in 1/8 in steps) with the differential each one produces at maximum and minimum flow — flagging plates that fall outside a usable range.

Every input field has its own unit selector, so US customary and metric units (in/mm, psi/kPa, °F/°C) can be mixed freely in the same calculation.

## The math behind it

| Standard | Used for |
|---|---|
| **AGA Report No. 3** (API MPMS Ch. 14.3 / ISO 5167) | Orifice discharge coefficient (Reader-Harris/Gallagher equation), expansion factor, and the overall flow equation |
| **AGA Report No. 8, Detail method** | Gas compressibility (Z), density, and molar mass from gas composition, temperature, and pressure |

The AGA 8 implementation is a direct JavaScript port of the reference source code published by the [National Institute of Standards and Technology (NIST)](https://github.com/usnistgov/AGA8), and its output has been checked against NIST's own published test case. The discharge coefficient calculation has been cross-checked against an independent open-source implementation.

This is an engineering estimating and cross-check tool. It is not a substitute for a certified flow computer where custody transfer or fiscal metering is involved.

## Installing on iPhone or Android

1. Open the app's link in a mobile browser (Safari or Chrome on iOS; Chrome on Android).
2. Tap **Share** (iOS) or the **⋮** menu (Android).
3. Tap **Add to Home Screen** (iOS) or **Install app** (Android).

Once installed, the app opens full-screen with its own icon and works with no internet connection — the page, fonts, and calculation engine are all cached on the device the first time it's opened.

## Project files

```
index.html             The app itself — interface, styles, and calculation engine in one file
manifest.webmanifest    App name, icon, and display settings used when installed
sw.js                   Service worker — caches the app so it runs offline
icon-192.png            Home screen icon (Android / general)
icon-512.png            Home screen icon (high resolution)
apple-touch-icon.png    Home screen icon (iOS)
```

Nothing is fetched from a server after the first load. There is no backend, no analytics, and no data collection — every calculation happens on-device.

## Local hosting

Any static file host with HTTPS will serve this app. Upload all six files to the same folder — for example, using [GitHub Pages](https://pages.github.com/), a home server, or any static hosting provider. HTTPS is required for the offline caching (service worker) to function.

## Limitations

- Covers orifice meters with flange, corner, or D–D/2 taps, per AGA 3. It does not cover venturi or V-cone meters.
- Standard plate sizing assumes 1/8 in bore increments and a beta ratio (bore ÷ pipe diameter) between 0.10 and 0.75, per the AGA 3 valid range.
- Gas composition supports the 21 components defined in the AGA 8 Detail method.

## Credits

- AGA 8 Detail method reference implementation: [NIST AGA8](https://github.com/usnistgov/AGA8) (public domain)
- Typeface: [Barlow](https://fonts.google.com/specimen/Barlow) family, licensed under the SIL Open Font License
