# Licensing of this Wine fork (LGPL branch `madeira-lgpl`)

This repository is a fork of [Wine](https://www.winehq.org/), which upstream
distributes under **LGPL-2.1-or-later**. This branch keeps that licence.

- Upstream code: LGPL-2.1-or-later, all upstream copyright and licence
  notices unchanged. Baseline: upstream tag `wine-11.4`.
- Modifications and new files authored for
  [Madeira](https://github.com/willfaust/Madeira): **LGPL-2.1-or-later**,
  Copyright (C) 2026 Will Faust, except the third-party contributions
  listed below. The new `dlls/wineios.drv` files are
  derived from upstream `winecoreaudio.drv` and keep its CodeWeavers and
  Huw Davies copyright notices.
- Provenance: the branch was rebuilt from the upstream baseline with the 51
  commits listed in the Madeira repository's `docs/wine-lgpl-provenance.md`,
  cherry-picked from the earlier GPL-converted branch with `-x` (each commit
  message names its origin). Later changes are committed on this branch
  directly. The earlier branch's LGPL-section-3 conversion to
  GPL-3.0 is NOT applied here; that conversion is irreversible for that
  copy, which is why this branch was rebuilt from the upstream baseline
  instead.
- Third-party contributions, **LGPL-2.1-or-later**, copyright retained by
  their authors, each signed off under the DCO (see `CONTRIBUTING.md`):
  - `feb96ad2be4` xinput: read Madeira host controller snapshots through
    win32u. Author: 125hz. Merged from pull request #1 on 2026-09-25.
  - The iOS WoW64 series, author 125hz, merged from pull requests #6-#12 on
    2026-09-29: `970dac54a4e` (WoW64 guest pointer conversion),
    `2ebe9374b26` (wow64win), `db62a711998` (unixlib wow64 thunks),
    `e9289051644` (ntdll per-thread WoW64), `1a73c698b8c` (win32u per-process
    state), `f9074408fd9` (server WoW64 thread contexts), `059cb1923c0` (AFD
    pointers, I/O status owner, volume serial).
  - `56f69bc7528` dinput: opt-in joystick backed by the Madeira host gamepad slot.
    Author: 125hz. Merged from pull request #3 on 2026-09-29.
  - `3ba35adcbdd` server iOS: queue a process-wide system APC on a live thread when
    none can be signalled. Author: 125hz. Merged from pull request #13 on
    2026-09-29.
  - Round 3, author 125hz, merged on 2026-09-30:
    `4e85de8c795`, `8d4c3d9ab5b`, `5c4d1f7a6f2` (nsi reads through the
    in-process fallback without `\\.\Nsi`, pull request #14);
    `c3119789ade` (server iOS: hand an undeliverable async I/O APC to a
    waiting thread, pull request #15); `e200a5e19a9`, `f6848ad4e98` (opt-in
    fastsync for events and semaphores, pull request #16); `d770df01ae7`
    (ntdll ARM64EC: opt-in guard against a self-deadlock in the loader's
    image-map notification, pull request #17).
  - Author spitefulowl, merged on 2026-10-04: `38aa753f98b` (ntdll ARM64EC:
    leave the syscall callback on the execute-request early return, pull
    request #22); `f2f3e4b42e4` (kernelbase iOS: GetTickCount and
    QueryInterruptTime from the performance counter, pull request #23);
    `f4bbccf9499` (ntdll ARM64EC: unwind data for x64 code running at a fixed
    base below 4 GB, pull request #24).
  - Author meshoklv, merged on 2026-10-05: `30efeaa807b` (ntdll: load the
    builtin XInput even when the game ships its own copy, pull request #19).
    Pull request #18 (`b7996f867cb`, ntdll ARM64EC: leave the syscall callback
    on the execute-request early return) is the same fix as `38aa753f98b`
    above and came first; it is recorded as merged with no change of its own.
  - Author bahacan16, merged on 2026-10-06: `67b8c8bed51` (xinput1_3 iOS:
    send XInputSetState motors to the host pad, pull request #20).
  - Author spitefulowl, merged on 2026-10-06: `000cac48452` (mscoree iOS:
    cooperative thread suspend and keep-delegates for Wine Mono, pull request
    #26).
  - opengl32: OpenGL ES contexts for Madeira's winios WGL driver
    (`dlls/opengl32/unix_wgl.c`) and the fixed low image base limited to x86
    builds (`dlls/opengl32/Makefile.in`). Author: Connor Gow, written with AI
    assistance, 2026-09-26. Carried as a patch in the Madeira repository
    (`patches/wine-opengl-winios.patch`).
  - opengl32: 32-bit (WoW64) callers on iOS. `make_opengl` makes the wow64
    thunks convert embedded guest pointers with `ios_wow_host_ptr()`, keeps
    handles and callbacks unchanged, and passes pointer-or-offset parameters
    unchanged while a buffer is bound (`dlls/opengl32/make_opengl`,
    regenerated `unix_thunks.c`, `unix_private.h`, `unix_wgl.c`). Author:
    Connor Gow, written with AI assistance, 2026-09-27. Carried in
    `patches/wine-opengl-winios.patch`.

  - Taken from Madeira's Wine fork (`willfaust/wine`, branch `madeira-lgpl`) after the two forks diverged on 2026-10-15, with the
    authors kept in the commit history; **LGPL-2.1-or-later**, copyright retained by the authors. The
    first hash is the commit in this fork, the second the same commit in Madeira's fork. Author Ixion, 2026-10-24: `40a6ae89eed`
    (`11f6aa3a931`), ntdll iOS: answer case-insensitive lookups from cached directory listings. Author ft7t8drgwf-wq (GitHub
    insertfloppy), 2026-10-28: `19bc4fe8994` (`3e1dcdfdaf6`), a directory cache per process, and `d58b0ea9c34` (`9a64361cce7`), read
    directories by path; 2026-10-30: `bd8c29cedfd` (`c0ad4a57a5a`), kernelbase: implement SetThreadIdealProcessorEx. Author 125hz,
    2026-11-01: `afa91d22c44` (`baaab873d22`), win32u: keep the Fonts values of the Windows directory's fonts. The pin moved to them on
    2026-11-05. The opengl32 commit `7aa1902adac` (2026-11-05) applies the patch `patches/wine-opengl-winios.patch` of Madeira's main
    repository (author Connor Gow, listed above) to this tree; its 1,956 added lines are the patch's.
  - Taken from Madeira's Wine fork (`willfaust/wine`, branch `madeira-lgpl`) on 2026-11-14, with the authors kept in the commit
    history; **LGPL-2.1-or-later**, copyright retained by the authors. The first hash is the commit in this fork, the second the same
    commit in Madeira's fork. Author Ash Hopkins, 2026-10-10: `6fc7d124af3` (`89481d27baf`), ntdll iOS: getsockopt, /dev/urandom and
    ReadFileScatter data reach buffers in RWX memory. Author SirDank, 2026-10-24: `7998dc112a9` (`929cc3690b3`), ntdll: accept
    SetNamedPipeHandleState on a pipe that is a plain unix fd (this fork's later commit `5aa5e3d2abd` limits it to the state such a
    pipe has). Author 125hz, 2026-10-12: `a46ac90cd8a` (`ef6c5cf183e`), setupapi iOS: ask for the media again only after
    FILEOP_NEWPATH. Author intraducine, 2026-10-26: the function `async_can_defer_to_issuer` of `server/async.c` and its use in
    `server/thread.c` come from `243c626d56f` (server: retain blocking I/O completions on the issuing thread); this fork's commit
    `7f9dbec02f1` puts them behind the switch `MADEIRA_APC_DEFER_ISSUER`, which is off by default.
  - Commits of Wine itself made after the 11.4 baseline, taken on 2026-11-14 from winehq's `master` (**LGPL-2.1-or-later**, copyright
    retained by their authors). Cherry-picked unchanged, the authors stay the commit authors; the first hash is the commit in this
    fork, the second Wine's: `cce7e9bf9ad` (`c8b71506800`), ntdll: Fall back to statfs if "important" free space is 0 on macOS, by
    Tim Clem, 2026-04-10; `6c9f03c73b0` (`35f715b4eff`), ntdll: Fix out-of-bounds access in NtQueryInformationToken, by Nikola
    Kuburović, 2026-09-12; `4a7d943a244` (`e3394292156`), ntdll: Avoid expensive inverted DST check on get_timezone_info() cache hit path,
    by Zhou Qiankang, 2026-03-16. Adapted: this fork's commit `239489424db` changes `_time64` and `_time32` of `dlls/msvcrt/time.c` as Wine's
    `0497d0ff62f` does (msvcrt: Avoid expensive timezone queries from plain time() calls, by Benjamin Fischer, 2026-05-14) and
    keeps the `_tzset_init()` call that Wine's commit drops.
  - This fork's own changes of 2026-11-14 to the commits listed in the two entries above (BCD; **LGPL-2.1-or-later** like the
    files they are in). `0a5f587e0d7`: the getsockopt, DONTFRAG and /dev/urandom parts of `6fc7d124af3` call the kernel on the
    caller's buffer first and take the local copy only after EFAULT; the NtReadFileScatter part of `6fc7d124af3` is unchanged, and in
    BCD it does not reach RWX memory (the helpers Madeira's unix side has for that are in Madeira's main repository and were not
    taken). `23e42159f72`: the media-loop change of `a46ac90cd8a` applies to setupapi's own default callback only
    (`MADEIRA_SETUPAPI_MEDIA_FIX` = 1: every callback, as in Madeira; 0: never). `aa9d15493b9`: `MADEIRA_APC_DEFER_ISSUER`
    (`7f9dbec02f1`) is read on every call. `8ac268308db`: the test for inverse daylight saving in `get_timezone_info`, the function
    `4a7d943a244` changes, asks for exactly one hour (the criterion comes from BCD's review of that commit).
  - Author 125hz, taken 2026-11-14 (willfaust/Madeira#575, willfaust/wine#71), in vkd3d-shader's `libs/vkd3d/libs/vkd3d-shader/fx.c`
    (vkd3d's own licence, LGPL-2.1-or-later): `1a5e1941899` (`8be7412f882`), 2026-11-04, the fx_2_0 writer emits sampler initializers,
    pass assignments and their resource records; `0f29e706b5c` (`ddf92babc5b`), 2026-11-05, numeric states carry every component, TRUE
    and FALSE beside a state's own names, a failed pass shader fails the effect.
  - This fork's own changes of 2026-11-14 to the commits of the entry above (BCD; **LGPL-2.1-or-later** like vkd3d-shader).
    `f0d271b5c6c`: every shader of an fx_2_0 effect is compiled from the state a freshly parsed context has
    (`reset_effect_compile_state`; before it, a later shader kept the literal constants, registers and samplers of the one compiled
    before), D3D bytecode only inside an fx_2_0 effect, and `MADEIRA_FX_WRITER` = 0 gives back the effect writer before the two
    commits byte for byte. `8f1e2c1d562`: the same reset before the shaders of fx_4_0 and fx_5_0 effects, which read their constant
    buffers behind the effect's layout before (vkd3d-shader's own writer, older than the two commits).

The LGPL permits combining this library with proprietary components (such
as Apple's Metal Shader Converter) subject to LGPL-2.1 section 6; see the
Madeira repository's `docs/LICENSING.md`.
