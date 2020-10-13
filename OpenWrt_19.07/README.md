OpenWrt / LEDE repository for OpenWrt_19.07
========
Binaries built from this repository on 2020-10-13 can be downloaded from https://arition.github.io/openwrt-repo/.
To add the repo, run
```
echo "src/gz arition_repo https://arition.github.io/openwrt-repo/OpenWrt_19.07" >> /etc/opkg/customfeeds.conf
opkg update 
```
You may also need to import the key of this repo. 
To import key, run

Openwrt 15.05 
```
opkg update; opkg install ca-certificates wget libopenssl
wget -O /tmp/805d030f380712aa https://arition.github.io/openwrt-repo/805d030f380712aa
opkg-key add /tmp/805d030f380712aa
```
LEDE 17.01 and later 
```
opkg update
opkg list-installed | grep -q uclient-fetch || opkg install uclient-fetch
opkg list-installed | grep -q libustream || opkg install libustream-mbedtls
wget -O /tmp/805d030f380712aa https://arition.github.io/openwrt-repo/805d030f380712aa
opkg-key add /tmp/805d030f380712aa
```

