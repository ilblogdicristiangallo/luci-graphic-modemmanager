# luci-graphic-modemmanager

**LuCI graphical interface for ModemManager (`mmcli`) on OpenWrt.**

Single-page LuCI app: modem status, **LTE** and **5G SA / 5G NSA** band lock (clickable green badges), diagnostics and configuration.

Bands are **read dynamically from the modem** (`supported-bands` / `current-bands`). Nothing is hardcoded — if the module has no 5G, SA/NSA tabs stay empty instead of forcing unsupported bands.

> **Packaging:** **APK** (OpenWrt 25.12 Alpine) **and IPK** (classic OpenWrt / opkg) will both be available.  
> More related projects are on the way (including the Flutter / Android companion app).

---

## Screenshots

Put PNG/WebP files in [`docs/screenshots/`](docs/screenshots/). Until a file exists, GitHub may show a broken image — replace as soon as you have captures.

| Modem(s) | LTE bands | 5G SA |
|:--------:|:---------:|:-----:|
| ![Modem(s)](docs/screenshots/01-modems.png) | ![LTE bands](docs/screenshots/02-lte-bands.png) | ![5G SA](docs/screenshots/03-5g-sa.png) |

| 5G NSA | Diagnostics | Configuration |
|:------:|:-----------:|:-------------:|
| ![5G NSA](docs/screenshots/04-5g-nsa.png) | ![Diagnostics](docs/screenshots/05-diagnostics.png) | ![Configuration](docs/screenshots/06-configuration.png) |

## Features

| Area | What you get |
|------|----------------|
| **Modem(s)** | Signal, operator, SIM, IMEI, ports, cell (MCC/MNC, TAC, Cell ID), LTE/5G RSRP–RSRQ–SNR |
| **Preferred LTE bands** | `eutran-*` → **B1, B3, B20…** — green = selected, grey = supported |
| **Preferred 5G SA bands** | `ngran-*` → **n28, n78, n258…** (only if the modem exposes NR) |
| **Preferred 5G NSA bands** | LTE anchor **B\*** + NR **n\*** in one apply (`eutran-3\|eutran-20\|ngran-78`) |
| **Diagnostics** | USB devices, tty/cdc-wdm ports, `mmcli` dump |
| **Configuration** | Modem index, refresh, BTS search site, restart modem / WAN |

Same UI style for LTE and 5G: clickable badges, green = on, grey = off.

# Apply always uses ModemManager:

```sh
mmcli -m 0 --set-current-bands="eutran-3|eutran-20"
mmcli -m 0 --set-current-bands="ngran-28|ngran-78"
mmcli -m 0 --set-current-bands="eutran-3|eutran-20|ngran-78"
mmcli -m 0 --set-current-bands="any"
