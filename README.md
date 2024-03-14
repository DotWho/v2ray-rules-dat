# 简介

[**V2Ray**](https://github.com/v2fly/v2ray-core) 路由规则文件加强版，可代替 V2Ray 官方 `geoip.dat` 和 `geosite.dat`，兼容 [Shadowsocks-windows](https://github.com/shadowsocks/shadowsocks-windows)、[Xray-core](https://github.com/XTLS/Xray-core)、[Trojan-Go](https://github.com/p4gefau1t/trojan-go)、[leaf](https://github.com/eycorsican/leaf) 和 [hysteria](https://github.com/apernet/hysteria)。使用 GitHub Actions 北京时间每天早上 6 点自动构建，保证规则最新。

## 规则文件生成方式

### geoip.dat

- 通过仓库 [@DotWho/geoip](https://github.com/DotWho/geoip) 生成
- 新增类别（方便有特殊需求的用户使用）：
  - `geoip:cloudflare`
  - `geoip:cloudfront`
  - `geoip:facebook`
  - `geoip:fastly`
  - `geoip:apple`
  - `geoip:google`
  - `geoip:netflix`
  - `geoip:telegram`
  - `geoip:twitter`

### geosite.dat

- 基于 [@v2fly/domain-list-community/data](https://github.com/v2fly/domain-list-community/tree/master/data) 数据，通过仓库 [@Loyalsoldier/domain-list-custom](https://github.com/Loyalsoldier/domain-list-custom) 生成
- **加入 AdRules 广告和隐私跟踪域名**：通过 [Adrules](https://adrules.top) 获取并加入到 `geosite:category-ads-all` 类别中
  - 关于使用方式，请参考下面 [geosite 的 Routing 配置方式](https://github.com/Loyalsoldier/v2ray-rules-dat#geositedat-1)

## 规则文件下载及使用方式

**下载地址**：

- **geoip-only-cn-private**：
  - [https://raw.githubusercontent.com/DotWho/geoip/release/geoip-only-cn-private.dat](https://raw.githubusercontent.com/DotWho/geoip/release/geoip-only-cn-private.dat)
- **geoip-asn.dat**：
  - [https://raw.githubusercontent.com/DotWho/geoip/release/geoip-asn.dat](https://raw.githubusercontent.com/DotWho/geoip/release/geoip-asn.dat)
- **geosite.dat**：
  - [https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/geosite.dat](https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/geosite.dat)
- **代理域名列表 proxy-list.txt**：
  - [https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/proxy-list.txt](https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/proxy-list.txt)
- **广告域名列表 reject-list.txt**：
  - [https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/reject-list.txt](https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/reject-list.txt)
- **Apple Proxy域名列表 apple-proxy.txt**：
  - [https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/apple-cn.txt](https://raw.githubusercontent.com/DotWho/v2ray-rules-dat/release/apple-proxy.txt)

### geosite.dat

跟 V2Ray 官方 `geosite.dat` 配置方式相同。相比官方 `geosite.dat` 文件，本项目特有的类别：
- `geosite:category-games@cn` 包含[category-games](https://github.com/v2fly/domain-list-community/blob/master/data/category-games) `steam`、`ea`、`blizzard`、`epicgames` 和 `nintendo` 等常见的游戏厂商。设置为直连，即可节省大量服务器流量。

## 致谢

- [@Loyalsoldier/geoip](https://github.com/Loyalsoldier/geoip)
- [@v2fly/domain-list-community](https://github.com/v2fly/domain-list-community)
- [@Loyalsoldier/domain-list-custom](https://github.com/Loyalsoldier/domain-list-custom)
- [@felixonmars/dnsmasq-china-list](https://github.com/felixonmars/dnsmasq-china-list)
- [@AdblockPlus/EasylistChina+Easylist.txt](https://easylist-downloads.adblockplus.org/easylistchina+easylist.txt)
- [@AdGuard/DNS-filter](https://kb.adguard.com/en/general/adguard-ad-filters#dns-filter)
