# Changelog

## Unreleased

- Drop `luci-app-passwall` and its translation package from the device config.
  `luci-app-openclash` already covers the same job, and PassWall's `SingBox`
  include was the only reason `sing-box` had to be pulled in twice.
- Add `vlmcsd` and `luci-app-vlmcsd` (Chinese translation included) so the
  router can serve KMS activation for Windows and Office clients on the LAN.
  Both are asserted in `REQUIRED_SELECTIONS`, so a silent `defconfig` drop now
  fails the build instead of shipping an image without KMS.
- Disable `SING_BOX_BUILD_NAIVE_OUTBOUND` in the device config. The `full`
  sing-box variant defaults this to `y` on aarch64, but `libcronet` is not part
  of the 25.12 feed any more, so the link step aborted the whole build with
  `ld.bfd: cannot find -lcronet`.

## 2.0.0 — 2026-11-02

Python rewrite of the ZeroWrt/MediaTek builder pipeline.

- Build source moved to `chasey-dev/immortalwrt-mt798x-rebase` `25.12`.
- Device selection is the MediaTek Builder config `configs/ruijie-rg-x60-new.config`
  (MTK U-Boot / mtkuboot layout).
- The shell `diy-script.sh` is replaced by Python modules:
  `customize.py`, `packages.py`, `patches.py`.
- Added `luci-app-ota` to the image, build metadata (`/etc/ota/build.json`),
  a schema-2 `ota.json`, `history.json`, and gh-pages publishing.
- LuCI patches `0001`–`0005` refreshed against `immortalwrt/luci`
  `openwrt-25.12`; GCC 16 patch `0006` retained.
- Added `SHA256SUMS`, `BUILD_INFO.txt`, `Packages.tar.gz` and
  `build.config` to the release artifacts.
- Added a memory-aware `nproc + 1` compile policy with serial `V=s` fallback.
- Added an optional toolchain cache in the `toolchain` release and a
  `Build Toolchain Cache` workflow.
- Unit tests and Ruff checks run on every pull request.
