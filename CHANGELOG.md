# Changelog

## Unreleased

- Keep `luci-app-openclash` as the only proxy front end. `luci-app-passwall`,
  `luci-app-homeproxy` and their translation packages are gone, and `sing-box`
  went with them because homeproxy was its only dependent. Beside dropping two
  duplicate proxy stacks, this also removes the `SING_BOX_BUILD_NAIVE_OUTBOUND`
  / `libcronet` link failure that used to abort the aarch64 build at the
  `Compile firmware` step.
- Add `vlmcsd` and `luci-app-vlmcsd` (Chinese translation included) so the
  router can serve KMS activation for Windows and Office clients on the LAN.
  Both packages are asserted in `REQUIRED_SELECTIONS`, so a silent `defconfig`
  drop now fails the build instead of shipping an image without KMS.
- Add `openlist2` and `luci-app-openlist2`. The AList LuCI package was archived
  in June 2025 and now points at OpenList as its successor, so the image ships
  the OpenList service plus its front end. It builds from source against the
  lite front-end dist to keep the image as small as possible.

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
