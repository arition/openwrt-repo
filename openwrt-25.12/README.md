# OpenWrt 25.12 repository

This repository provides `vlmcsd` and `luci-app-vlmcsd` as APK packages for
OpenWrt 25.12. Run the following commands as root on your router.

## Check your release and architecture

```sh
cat /etc/openwrt_release
apk --print-arch
```

Use this repository only with OpenWrt 25.12. Available package architectures:

- `aarch64_cortex-a53`
- `aarch64_cortex-a72`
- `arm_cortex-a15_neon-vfpv4`
- `arm_cortex-a9_vfpv3-d16`
- `mips_24kc`
- `mipsel_24kc`
- `x86_64`

## Import the APK signing key

```sh
mkdir -p /etc/apk/keys
wget -O /tmp/arition-repo.pem https://arition.github.io/openwrt-repo/arition-repo.pem &&
  cp /tmp/arition-repo.pem /etc/apk/keys/arition-repo.pem
```

The [public key](../arition-repo.pem) is for APK repository signatures.
The older `805d030f380712aa` usign key and `opkg-key add` command do not apply
to OpenWrt 25.12.

## Add the repository

The commands below detect the package architecture and add the feed only if
it is not already present. Keep the official OpenWrt repositories enabled for
package dependencies.

```sh
arch="$(apk --print-arch)"
feed="https://arition.github.io/openwrt-repo/openwrt-25.12/$arch/packages.adb"
mkdir -p /etc/apk/repositories.d
grep -qxF "$feed" /etc/apk/repositories.d/customfeeds.list 2>/dev/null ||
  printf '%s\n' "$feed" >> /etc/apk/repositories.d/customfeeds.list
apk update
```

The feed URL must end in `packages.adb`. Do not add an opkg-style `src/gz`
prefix or point a 25.12 router at an older IPK feed.

## Install

Install the LuCI interface and its `vlmcsd` dependency:

```sh
apk add luci-app-vlmcsd
```

For the daemon without the LuCI interface, use `apk add vlmcsd` instead.

If `apk update` reports an untrusted signature, check that the APK public key
was downloaded successfully into `/etc/apk/keys/`. A 404 for `packages.adb`
usually means the architecture is not in the list above or the feed URL is
incorrect.

[All releases](../)
