# Verified Android 6 baseline

Selected baseline: the combined **IronFox v159.0 + Tor Browser 15.0.24** stack.

Why this combined baseline:
- **IronFox v159.0** is the selected Firefox-derived Android compatibility baseline for Toph.
- **Tor Browser 15.0.24** is the locked upstream build and validation baseline recorded in `VERSION.lock`.
- Tor Browser 15.0 is based on Firefox ESR 140.
- Tor Browser 15.0.24 updates Android GeckoView to Firefox ESR 140.17.0.
- Tor Browser 15.x is the final major Tor Browser series supporting Android 5, 6, and 7.
- Tor Browser 16 drops Android versions older than 8.0.

Compatibility note:
- **IronFox v159.0** is the Firefox baseline and compatibility guide.
- **Tor Browser 15.0.24** remains the exact project lock and build reference.
- The two are intentionally combined: IronFox defines the Firefox-derived Android target, and Tor Browser defines the reproducible upstream integration stack.

## Locked revisions

| Component | Version | Revision |
|---|---|---|
| Tor Browser | 15.0.24 | 8cae94965791def3a7e63a1acb9e998ce8133de9 |
| Base Browser | Firefox ESR 140.17.0 | c62d7c244409d6d6ca37cd7f4819260ffc3cf60b |
| Fenix/Tor Browser Android source | release build dependency | 61d9e9dc2c94ca0e071ce3be0b018c5a5958101f |
| Tor | 0.4.9.13 | tor-0.4.9.13 |

## Important distinction

The Tor Browser repository is a Firefox-derived source tree. The Base Browser and Tor Browser revisions above are therefore the authoritative source revisions for the locked build baseline.

IronFox v159.0 is the Firefox-derived Android compatibility baseline selected for Toph work. It does not replace the locked build revision set. The project's exact version lock remains the authoritative implementation baseline, while IronFox provides the Android compatibility model.

## Android 6 target

Toph's target is Android 6 / API 23.

The combined baseline uses **IronFox v159.0** for Firefox-derived Android compatibility logic and **Tor Browser 15.0.24** for the exact integrated build path and runtime validation on API 23.

## Next validation steps

1. Fetch the exact upstream repositories.
2. Check out the locked Tor Browser/Base Browser revisions.
3. Reproduce the upstream Android build environment.
4. Build without Toph patches first.
5. Test installation/startup/page loading on API 23.
6. Only after that, add Toph privacy and network-mode patches.
