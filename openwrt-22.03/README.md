# OpenWrt / LEDE repository for openwrt-22.03

Binaries built from this repository can be downloaded from https://arition.github.io/openwrt-repo/.

To add the repo, run

```sh
echo "src/gz arition_repo https://arition.github.io/openwrt-repo/openwrt-22.03/<your-router-arch>" >> /etc/opkg/customfeeds.conf
opkg update 
```

You may also need to import the key of this repo. 
To import key, run

```sh
opkg update
opkg list-installed | grep -q uclient-fetch || opkg install uclient-fetch
opkg list-installed | grep -q libustream || opkg install libustream-mbedtls
wget -O /tmp/805d030f380712aa https://arition.github.io/openwrt-repo/805d030f380712aa
opkg-key add /tmp/805d030f380712aa
```

