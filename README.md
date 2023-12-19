# 简介

[**V2Ray**](https://github.com/v2fly/v2ray-core) 路由规则文件加强版，可代替 V2Ray 官方 `geoip.dat` 和 `geosite.dat`，兼容 [Shadowsocks-windows](https://github.com/shadowsocks/shadowsocks-windows)、[Xray-core](https://github.com/XTLS/Xray-core)、[Trojan-Go](https://github.com/p4gefau1t/trojan-go)、[leaf](https://github.com/eycorsican/leaf) 和 [hysteria](https://github.com/apernet/hysteria)。使用 GitHub Actions 北京时间每天早上 6 点自动构建，保证规则最新。

## 规则文件生成方式

### geoip.dat

- 通过仓库 [@Loyalsoldier/geoip](https://github.com/Loyalsoldier/geoip) 生成
- 新增类别（方便有特殊需求的用户使用）：
  - `geoip:cloudflare`
  - `geoip:cloudfront`
  - `geoip:facebook`
  - `geoip:fastly`
  - `geoip:google`
  - `geoip:netflix`
  - `geoip:telegram`
  - `geoip:twitter`

### geosite.dat

- 基于 [@v2fly/domain-list-community/data](https://github.com/v2fly/domain-list-community/tree/master/data) 数据，通过仓库 [@Loyalsoldier/domain-list-custom](https://github.com/Loyalsoldier/domain-list-custom) 生成
- **加入大量中国大陆域名、Apple 域名和 Google 域名**：
  - [@felixonmars/dnsmasq-china-list/accelerated-domains.china.conf](https://github.com/felixonmars/dnsmasq-china-list/blob/master/accelerated-domains.china.conf) 加入到 `geosite:cn` 类别中
  - [@felixonmars/dnsmasq-china-list/apple.china.conf](https://github.com/felixonmars/dnsmasq-china-list/blob/master/apple.china.conf) 加入到 `geosite:geolocation-!cn` 类别中（如希望本文件中的 Apple 域名直连，请参考下面 [geosite 的 Routing 配置方式](https://github.com/Loyalsoldier/v2ray-rules-dat#geositedat-1)）
  - [@felixonmars/dnsmasq-china-list/google.china.conf](https://github.com/felixonmars/dnsmasq-china-list/blob/master/google.china.conf) 加入到 `geosite:geolocation-!cn` 类别中（如希望本文件中的 Google 域名直连，请参考下面 [geosite 的 Routing 配置方式](https://github.com/Loyalsoldier/v2ray-rules-dat#geositedat-1)）
- **加入 AdGuard DNS Filter 广告域名**：通过 [@AdGuard/DNS-filter](https://kb.adguard.com/en/general/adguard-ad-filters#dns-filter) 获取并加入到 `geosite:category-ads-all` 类别中
- **加入 AdRules 广告和隐私跟踪域名**：通过 [Adrules](https://adrules.top) 获取并加入到 `geosite:category-ads-all` 类别中
  - 关于这三个类别的使用方式，请参考下面 [geosite 的 Routing 配置方式](https://github.com/Loyalsoldier/v2ray-rules-dat#geositedat-1)
- **可添加自定义直连、代理和广告域名**：由于上游域名列表更新缓慢或缺失某些域名，所以引入**需要添加的域名**列表。[`hidden 分支`](https://github.com/Loyalsoldier/v2ray-rules-dat/tree/hidden)里的三个文件 `direct.txt`、`proxy.txt` 和 `reject.txt`，分别存放自定义的需要添加的直连、代理、广告域名，最终分别加入到 `geosite:cn`、`geosite:geolocation-!cn` 和 `geosite:category-ads-all` 类别中
- **可移除自定义直连、代理和广告域名**：由于上游域名列表存在需要被移除的域名，所以引入**需要移除的域名**列表。[`hidden 分支`](https://github.com/Loyalsoldier/v2ray-rules-dat/tree/hidden)里的三个文件 `direct-need-to-remove.txt`、`proxy-need-to-remove.txt` 和 `reject-need-to-remove.txt`，分别存放自定义的需要从 `direct-list`（直连域名列表）、`proxy-list`（代理域名列表）和 `reject-list`（广告域名列表） 移除的域名

## 规则文件下载及使用方式

**下载地址**：

- **geoip-only-cn-private**：
  - [https://raw.githubusercontent.com/Loyalsoldier/geoip/release/geoip-only-cn-private.dat](https://raw.githubusercontent.com/Loyalsoldier/geoip/release/geoip-only-cn-private.dat)
- **geoip-asn.dat**：
  - [https://raw.githubusercontent.com/Loyalsoldier/geoip/release/geoip-asn.dat](https://raw.githubusercontent.com/Loyalsoldier/geoip/release/geoip-asn.dat)
- **geoip.dat**：
  - [https://raw.githubusercontent.com/Loyalsoldier/geoip/release/geoip.dat](https://raw.githubusercontent.com/Loyalsoldier/geoip/release/geoip.dat)
- **geosite.dat**：
  - [https://github.com/DotWho/v2ray-rules-dat/releases/latest/download/geosite.dat](https://github.com/DotWho/v2ray-rules-dat/releases/latest/download/geosite.dat)
- **直连域名列表 direct-list.txt**：
  - [https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/direct-list.txt](https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/direct-list.txt)
- **代理域名列表 proxy-list.txt**：
  - [https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/proxy-list.txt](https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/proxy-list.txt)
- **广告域名列表 reject-list.txt**：
  - [https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/reject-list.txt](https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/reject-list.txt)
- **Apple 在中国大陆可直连的域名列表 apple-cn.txt**：
  - [https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/apple-cn.txt](https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/apple-cn.txt)
- **Google 在中国大陆可直连的域名列表 google-cn.txt**：
  - [https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/google-cn.txt](https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/google-cn.txt)

### geosite.dat

跟 V2Ray 官方 `geosite.dat` 配置方式相同。相比官方 `geosite.dat` 文件，本项目特有的类别：
- `geosite:apple-cn`：包含 [@felixonmars/dnsmasq-china-list/apple.china.conf](https://github.com/felixonmars/dnsmasq-china-list/blob/master/apple.china.conf) 文件里的域名，供希望 Apple 域名直连（不走代理）的用户使用。
- `geosite:google-cn`：包含 [@felixonmars/dnsmasq-china-list/google.china.conf](https://github.com/felixonmars/dnsmasq-china-list/blob/master/google.china.conf) 文件里的域名，供希望 Google 域名直连（不走代理）的用户使用。
- `geosite:category-games@cn` 包含[category-games](https://github.com/v2fly/domain-list-community/blob/master/data/category-games) `steam`、`ea`、`blizzard`、`epicgames` 和 `nintendo` 等常见的游戏厂商。设置为直连，即可节省大量服务器流量。

> ⚠️ 注意：在 Routing 配置中，类别越靠前（上），优先级越高，所以 `geosite:apple-cn` 和 `geosite:google-cn` 要放置在 `geosite:geolocation-!cn` 前（上）面才能生效。

## 致谢

- [@Loyalsoldier/geoip](https://github.com/Loyalsoldier/geoip)
- [@v2fly/domain-list-community](https://github.com/v2fly/domain-list-community)
- [@Loyalsoldier/domain-list-custom](https://github.com/Loyalsoldier/domain-list-custom)
- [@felixonmars/dnsmasq-china-list](https://github.com/felixonmars/dnsmasq-china-list)
- [@AdblockPlus/EasylistChina+Easylist.txt](https://easylist-downloads.adblockplus.org/easylistchina+easylist.txt)
- [@AdGuard/DNS-filter](https://kb.adguard.com/en/general/adguard-ad-filters#dns-filter)
