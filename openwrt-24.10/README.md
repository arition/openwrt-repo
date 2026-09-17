# OpenWrt 24.10 repository

This archived feed provides IPK packages for OpenWrt 24.10. For OpenWrt
25.12, use the [APK installation instructions](../openwrt-25.12/) instead.

Available architectures: `aarch64_cortex-a53`, `arm_cortex-a15_neon-vfpv4`,
`arm_cortex-a9_vfpv3-d16`, `mips_24kc`, `mipsel_24kc`, and `x86_64`.

Run these commands as root on a router running OpenWrt 24.10.

## Import the opkg signing key

```sh
wget -O /tmp/805d030f380712aa https://arition.github.io/openwrt-repo/805d030f380712aa &&
  opkg-key add /tmp/805d030f380712aa
```

## Add the repository and install

Find your package architecture with `opkg print-architecture`. Replace
`<your-router-arch>` below with a supported architecture from the list above,
then add the feed once:

```sh
echo "src/gz arition_repo https://arition.github.io/openwrt-repo/openwrt-24.10/<your-router-arch>" >> /etc/opkg/customfeeds.conf
opkg update
opkg install luci-app-vlmcsd
```

The LuCI package installs `vlmcsd` as a dependency. For the daemon alone, use
`opkg install vlmcsd`.

[All releases](../)
