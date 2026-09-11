# OrgSuite Trust Policy — Apple Root Store

**Status: Completed (policy document)**  
**Canonical Apple article:** https://support.apple.com/en-us/103272  
**Current Apple list:** https://support.apple.com/en-us/126047

## Purpose

Define how OrgSuite products, agents, Shortcuts, Device Management profiles, Vercel/Node backends, and workplace devices trust TLS and code-signing certificates when they run on or talk to Apple platforms.

## Rules

1. **Use the platform Root Store.** iOS, iPadOS, macOS, tvOS, visionOS, and watchOS already ship Apple's Root Store. OrgSuite clients on those OSes must use the system trust store. Do not bundle a parallel public-root bundle unless a non-Apple runtime requires one (for example Node on Linux using Mozilla/OpenSSL defaults).

2. **Do not re-install Apple roots in Configuration Profiles.** Apple states these Root CA certificates do not need to be included in Configuration Profiles. OrgSuite MDM / Apple Configurator / Device Management payloads must not duplicate Apple system roots.

3. **Do not invent OrgSuite root CAs for public TLS.** Public websites (`*.vercel.app`, custom domains on GoDaddy) must use publicly trusted CAs already in Apple's store (for example Let's Encrypt, Amazon, Google Trust Services, DigiCert, Sectigo/USERTrust). Do not stand up a private OrgSuite root and expect Safari or Mail to trust it without a managed profile that the owner has explicitly approved.

4. **Private / enterprise CAs require an explicit profile.** If PSE Management ever needs an internal CA, document it here first, ship it only via a signed Configuration Profile, and keep the private key off GitHub.

5. **Pinning is opt-in and reviewed.** Certificate or public-key pinning is allowed only for a named OrgSuite backend after a design review. Default is system-store validation + hostname checks.

6. **No secrets in this repository.** No private keys, `.p12`, Apple Push certificates, App Store Connect API keys, or MDM vendor certs. Those stay in host Keychain, Vercel env, or Firebase Secret Manager.

7. **Refresh from Apple, not from memory.** When Apple publishes a new shared Root Store (new support article ID), update `sources.json` and the README table. Treat Apple's version string (currently recorded as `2025082000`) as authoritative.

8. **Android and Linux runtimes.** Family Manager / Tasker / Termux / Vercel Node do not use Apple's store. They use the platform or OpenSSL/Mozilla store. Do not assume an Apple-only root exists on those hosts.

## OrgSuite surfaces this policy covers

| Surface | Trust store | Status |
|---------|-------------|--------|
| Safari / WebKit on owner Apple devices | Apple Root Store | Available |
| Working Copy, Shortcuts, Apple Intelligence | Apple Root Store | Available |
| OrgSuite native Apple apps (`orgsuite-apple-platform`) | Apple Root Store via URLSession / Network.framework | Ready to Configure in app code |
| Vercel / Node backends | Platform CA bundle (not Apple) | Available |
| Android Family Manager devices | Android system store | Available |
| Custom MDM profiles | Must not re-embed Apple roots | Proposed until a profile is authored |

## Verification checklist

- [ ] Production domains present a chain to a CA listed on Apple's current page.
- [ ] No OrgSuite Configuration Profile contains copies of Apple system roots.
- [ ] No private keys committed to this or related public repos.
- [ ] `sources.json` `appleCurrentArticle` still resolves to 200.
- [ ] When Apple ships a new shared store, README archive table is updated the same day it is noticed.

## Related official Apple documents

- Available root certificates — https://support.apple.com/en-us/103272
- Current list (Trust Store 2025082000) — https://support.apple.com/en-us/126047
- Configuration Profiles — https://support.apple.com/guide/apple-configurator-mac/create-and-edit-configuration-profiles-pmd85719196/mac
- Contact vendor disclaimer page — https://support.apple.com/103190
