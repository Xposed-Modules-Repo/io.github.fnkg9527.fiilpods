<div align="center">

# FiilPods

**FIIL earbuds, integrated into Xiaomi HyperOS like first-party ones**

</div>

---

## What it is

HyperOS only exposes its native earbud experience — the fusion-device-center card, the Bluetooth detail page, the super island, wear detection, system-level ANC switching — to Xiaomi's own earbuds. Plug in a pair of FIIL buds and the system sees a generic Bluetooth headset.

FiilPods is an LSPosed module that injects into the system Bluetooth process, speaks FIIL's own protocol over classic Bluetooth SPP (RFCOMM) and BLE GATT, and translates the results into what MIUI/HyperOS understands. After installing it, FIIL earbuds present themselves to the system the way a Xiaomi pair would.

The module does not draw its own overlay, does not keep a foreground service, and does not take over the notification shade — every surface is the system's own.

## Features

| Capability | Detail |
| --- | --- |
| Fusion device center | The headset card in the control center, with live ANC/transparency and icon updates |
| Bluetooth detail page | Battery, firmware, model, ANC, EQ, spatial audio, LDAC switch |
| Focus notification / super island | Native prompts for connect and battery changes |
| Wear detection | Pause when removed, resume when worn |
| ANC | The system-level noise-control API drives FIIL's own protocol commands |
| LDAC | Adds the earbud-side switch that the official app keeps hidden, and reads back the unlock state |
| Model artwork | Shows the official product image for the detected model; headphones and earbuds get different icons in the fusion center |
| Device identity | Optionally present as a supported model so the system exposes switches it would otherwise hide |

## Supported devices

FIIL's earbud and headphone line, identified by `earType`. Verified on FIIL Key Max (headphones, RFCOMM Mate protocol). The protocol family splits into GAIA and Mate branches, auto-detected per model.

Other brands are out of scope; the same author's HuaweiPods and HyperPods cover Huawei and AirPods respectively.

## Installation

1. Requires LSPosed (or a compatible libxposed API 102 framework).
2. Install the module, **enable** it in LSPosed, and scope it to:
   `com.android.bluetooth`, `com.xiaomi.bluetooth`, `com.milink.service`, `com.android.settings`
3. **Toggle Bluetooth off and on** (or reboot) after installing or changing the scope — LSPosed injects at process start, so hooks will not take effect until the Bluetooth process restarts.
4. Connect the FIIL earbuds and open the module app to confirm the connection state.

## Known limitations

- The status-bar small icon stays the system Bluetooth glyph: the official model images are opaque colour product shots, and Android tints status-bar icons by alpha, so a silhouette loses all detail.
- LDAC requires the earbuds' high-resolution audio to be unlocked first (the step inside the official FIIL+ app). The detail page tells you when it is not.
- Model detection relies on `earType`; a model that is not in the table can be selected manually in settings.

## Links

- Source and issue tracker: <https://github.com/FNKG9527/FiilPods>
- Changelog: <https://github.com/FNKG9527/FiilPods/blob/main/CHANGELOG.md>
- Third-party licenses: [THIRD_PARTY_LICENSES.md](https://github.com/FNKG9527/FiilPods/blob/main/THIRD_PARTY_LICENSES.md)

## Acknowledgements

The UI and project skeleton come from [OppoPods](https://github.com/1812z/OppoPods); the hook infrastructure follows [HuaweiPods](https://github.com/Nshpiter/HuaweiPods); the super-island shapes follow [HyperPods](https://github.com/Art-Chen/HyperPods). Protocol facts were reverse engineered from the official FIIL+ app and the MiLink system component.

Released under GPL-3.0.
