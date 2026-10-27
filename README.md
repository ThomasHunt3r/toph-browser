# Toph Browser
![logo](Duck-ai-image-2026-10-05-21-53_edited.jpg)
**TOPH = The Onion Phox**

Toph Browser is a privacy-focused Firefox-derived Android browser project targeting **Android 6 (API 23)**.

## Combined compatibility baseline

Toph uses the combined **IronFox v159.0 + Tor Browser 15.0.24** baseline.

- **IronFox v159.0** is the Firefox-derived Android compatibility baseline and the primary browser-version target for compatibility work.
- **Tor Browser 15.0.24** remains the locked upstream integration and verification stack recorded in `VERSION.lock`.
- The Tor Browser lock stays authoritative for exact source and build verification, while IronFox v159.0 provides the Firefox-derived Android compatibility model used to adapt the stack.

## Project goals

- Firefox/Gecko-based browsing.
- Android 6 compatibility.
- Telemetry and unnecessary remote-data collection removed or disabled where practical.
- Tor integration with an explicit network-mode design.
- Support for the public Tor network and a separately configured private/custom Tor network.
- Reproducible, auditable upstream revisions and local patches.

## Repository layout

```text
toph-browser/
├── README.md
├── VERSION.lock
├── .gitignore
├── upstream/
│   ├── firefox/
│   ├── tor/
│   └── tor-browser/
├── patches/
│   ├── android6/
│   ├── telemetry/
│   ├── browser-ui/
│   └── tor-config/
├── config/
│   ├── official-network/
│   ├── custom-network/
│   └── privacy/
├── scripts/
├── build/
└── tests/
```

The large Mozilla and Tor source trees are intentionally **not vendored** into this repository. They should be fetched from their official upstream repositories at the exact revisions recorded in `VERSION.lock`, with the project compatibility work aligned to the combined **IronFox v159.0 + Tor Browser 15.0.24** baseline.

## Upstream sources

- IronFox: https://gitlab.com/ironfox-oss/IronFox/-/tree/v159.0?ref_type=heads
- Tor Browser: https://gitlab.torproject.org/tpo/applications/tor-browser
- Tor: https://gitlab.torproject.org/tpo/core/tor
- Firefox: https://github.com/mozilla-firefox/firefox

## Android 6

Android 6 corresponds to **API 23**. Compatibility must be established by the selected Android-compatible Firefox-derived baseline, the build configuration, dependencies, manifest requirements, and validation on the supported API level. Toph uses the combined **IronFox v159.0 + Tor Browser 15.0.24** baseline: IronFox is the Firefox compatibility model and Tor Browser is the locked upstream integration stack.

## Network modes

Toph should keep the public and custom Tor environments conceptually separate:

1. **Official Tor** — connects through the public Tor network.
2. **Custom Tor** — connects to a separately operated Tor environment with its own authorities/relays and configuration.

Switching modes must account for browser connection reuse, DNS handling, Tor process state, and isolation. A private Tor network is not automatically equivalent to the anonymity properties of the public Tor network.

## Privacy approach

Privacy work should be auditable rather than relying on a blanket blocklist. The project should audit:

- telemetry and analytics;
- crash/error reporting;
- remote configuration and studies;
- unnecessary network endpoints;
- update and discovery services;
- DNS and connection behavior;
- third-party services.

Changes belong in focused patches under `patches/` and should be accompanied by tests or audit notes.

## Build workflow

1. Clone the upstream repositories into `upstream/`.
2. Select release tags that are actually compatible with the Android 6 requirement.
3. Record exact tags and commit SHAs in `VERSION.lock`.
4. Bootstrap the matching Mozilla build environment.
5. Apply only the patches required for Android 6 and Toph privacy/Tor behavior.
6. Build and test on an Android 6 device or emulator.
7. Record compatibility and test results under `tests/`.

No upstream revision hashes are invented in this repository. Exact revisions should be resolved from upstream before implementation begins. Toph's effective project baseline is the combined **IronFox v159.0 + Tor Browser 15.0.24** stack, with Tor Browser remaining the exact locked build reference.

## Status

This repository currently contains the project scaffold and documentation. It does **not** yet contain the full Firefox/Tor source trees or a claimed working Android 6 build.

## License

This project will need to preserve the applicable upstream Mozilla, Tor, and other third-party licenses/notices as implementation proceeds.
