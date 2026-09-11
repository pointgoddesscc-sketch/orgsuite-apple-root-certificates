# OrgSuite Apple Root Certificates

**Status: Completed / Live (documentation)**  
**Apple source of truth: [support.apple.com/en-us/103272](https://support.apple.com/en-us/103272)**

This repository is OrgSuite's counterpart to Apple Support article **103272** — *Available root certificates for Apple operating systems*.

Apple publishes the Root Stores that ship with iOS, iPadOS, macOS, tvOS, visionOS, and watchOS. Those Root CA certificates validate TLS and code-signing chains on Apple devices. OrgSuite does **not** replace Apple's Root Store. This repo indexes Apple's official lists, records how OrgSuite products must use them, and keeps a workplace-owned copy of the index so we are not dependent on a single support URL remaining unchanged.

## Live Surfaces

| Surface | Status | URL |
|---------|--------|-----|
| GitHub (OrgSuite index) | **Completed / Live** | https://github.com/pointgoddesscc-sketch/orgsuite-apple-root-certificates |
| Apple article (canonical) | **Connected** | https://support.apple.com/en-us/103272 |
| Current Apple Root Store list | **Connected** | https://support.apple.com/en-us/126047 |
| OrgSuite trust policy | **Completed** | [docs/ORGSUITE-TRUST-POLICY.md](./docs/ORGSUITE-TRUST-POLICY.md) |
| Structured source index | **Completed** | [sources.json](./sources.json) |
| Static HTML viewer | **Completed** (in-repo) | [index.html](./index.html) |

## About certificates (OrgSuite wording)

Root Stores contain Root CA certificates preinstalled with Apple operating systems.

Root CA certificates establish a validation chain that verifies other certificates signed by the included roots — for example, to establish a secure connection to a web server, API, or App Store signed binary.

When IT administrators create [Configuration Profiles](https://support.apple.com/guide/apple-configurator-mac/create-and-edit-configuration-profiles-pmd85719196/mac), Apple's preinstalled Root CA certificates do **not** need to be included. OrgSuite MDM / Device Management profiles must follow the same rule.

## Current Root Store (Apple)

**Trust Store version recorded here:** `2025082000`  
**Applies to (Apple's current shared store):** iOS 26, iPadOS 26, macOS 26, tvOS 26, visionOS 26, watchOS 26 and later.

Full certificate table (name, issuer, type, key size, signature algorithm, serial, expiry, fingerprint) lives only on Apple:

- [List of available root certificates in iOS 26, iPadOS 26, macOS 26, tvOS 26, visionOS 26 and watchOS 26](https://support.apple.com/en-us/126047)

Beginning with iOS 12, macOS 10.14, tvOS 12, and watchOS 5, all Apple operating systems use a **shared** Root Store. When Apple updates the store, previous versions are archived at the links below.

### How to check the Root Store version on a device

**iPhone / iPad**

1. Settings → General → About → Certificate Trust Settings (wording may vary by OS version).
2. Or follow the steps on Apple's current list page.

**Mac**

1. Finder / Keychain Access → System Roots.
2. Compare against the version noted on Apple's current list page.

OrgSuite staff should treat Apple's published version string as authoritative. Do not invent a local version number.

## Previous shared Root Stores (Apple archives)

| Apple OS set | Official list |
|--------------|---------------|
| iOS 18 / iPadOS 18 / macOS 15 / tvOS 18 / visionOS 2 / watchOS 11 | https://support.apple.com/en-us/121672 |
| iOS 17.4 / iPadOS 17.4 / macOS 14.4 / tvOS 17.4 / visionOS 1.1 / watchOS 10.4 | https://support.apple.com/en-us/121728 |
| iOS 17 / iPadOS 17 / macOS 14 / tvOS 17 / watchOS 10 | https://support.apple.com/en-us/105116 |
| iOS 16.5 / iPadOS 16.5 / macOS 13.5 / tvOS 16.5 / watchOS 9.5 | https://support.apple.com/en-us/102666 |
| iOS 16 / iPadOS 16 / macOS 13 / tvOS 16 / watchOS 9 | https://support.apple.com/en-us/103100 |
| iOS 15.1 / iPadOS 15.1 / macOS 12.1 / tvOS 15.1 / watchOS 8.1 | https://support.apple.com/en-us/103254 |
| iOS 15 / iPadOS 15 / macOS 12 / tvOS 15 / watchOS 8 | https://support.apple.com/en-us/103252 |
| iOS 14.2 / iPadOS 14.2 / macOS 11 / tvOS 14.2 / watchOS 7.1 | https://support.apple.com/en-us/103251 |
| iOS 14.0 / macOS 11.0 / tvOS 14.0 / watchOS 7.0 | https://support.apple.com/en-us/103248 |
| iOS 13.4 / macOS 10.15.4 / tvOS 13.4 / watchOS 6.2 | https://support.apple.com/en-us/103249 |
| iOS 13 / iPadOS 13 / macOS 10.15 / tvOS 13 / watchOS 6 | https://support.apple.com/en-us/103243 |
| iOS 12.1.3 / macOS 10.14.3 / tvOS 12.1.2 / watchOS 5.1.3 | https://support.apple.com/en-us/103242 |
| iOS 12 / macOS 10.14 / tvOS 12 / watchOS 5 | https://support.apple.com/en-us/103247 |

## Archived Root Stores (pre-shared)

### iOS

- iOS 11 — https://support.apple.com/kb/HT208125
- iOS 10 — https://support.apple.com/kb/HT207177
- iOS 9 — https://support.apple.com/kb/HT205205
- iOS 8 — https://support.apple.com/kb/HT205214
- iOS 7 — https://support.apple.com/kb/HT203065

### macOS

- macOS High Sierra — https://support.apple.com/kb/HT208127
- macOS Sierra — https://support.apple.com/kb/HT207189
- OS X El Capitan — https://support.apple.com/kb/HT205204
- OS X Yosemite — https://support.apple.com/kb/HT205218
- OS X Mavericks — https://support.apple.com/kb/HT203120

### watchOS

- watchOS 4 — https://support.apple.com/kb/HT208128
- watchOS 3 — https://support.apple.com/kb/HT207190
- watchOS 2 — https://support.apple.com/kb/HT205203
- Watch OS — https://support.apple.com/kb/HT205216

### tvOS

- tvOS 11 — https://support.apple.com/kb/HT208129
- tvOS 10 — https://support.apple.com/kb/HT207232

## What this repo is *not*

- Not a fork of Apple's Root Store.
- Not a place to store `.p12`, `.pem` private keys, Apple Developer certificates, or MDM push certs (those belong in Keychain / host secret managers only).
- Not a substitute for [orgsuite-beta-developer-certificate](https://github.com/pointgoddesscc-sketch/orgsuite-beta-developer-certificate) (Apple developer / beta signing guidance).
- Not a full dump of every SHA-256 fingerprint. Fingerprints change with Apple's store; always open the official list.

## Related OrgSuite repos

- [orgsuite-beta-developer-certificate](https://github.com/pointgoddesscc-sketch/orgsuite-beta-developer-certificate) — developer / beta signing guidance
- [orgsuite-apple-platform](https://github.com/pointgoddesscc-sketch/orgsuite-apple-platform) — native Apple apps + Device Management
- [orgsuite-ios-licenses-acknowledgements](https://github.com/pointgoddesscc-sketch/orgsuite-ios-licenses-acknowledgements)
- [orgsuite-canary-ios-acknowledgements](https://github.com/pointgoddesscc-sketch/orgsuite-canary-ios-acknowledgements)
- [orgsuite-workspace](https://github.com/pointgoddesscc-sketch/orgsuite-workspace)

## Attribution

Apple product names and support article text remain Apple's. This repo is an OrgSuite workplace index and trust-policy document. Information about third-party CAs is provided only as Apple publishes it; OrgSuite does not endorse those CAs independently.

**Created:** 2026-09-11  
**Owner account:** pointgoddesscc-sketch / pointgoddesscc@gmail.com  
**Workplace:** PSE Management → OrgSuite Codex App
