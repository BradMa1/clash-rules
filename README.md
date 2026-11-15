# clash-rules

自建节点用的 clash / 小火箭 极简配置模板，规则集走 MetaCubeX 官方源，不依赖任何固定 VPS。

## 目录

```
clash-rules/
├── config.example.yaml        # Clash 极简配置（mihomo：手动/自动 + 全局开关 + 国内直连）
├── shadowrocket.example.conf  # 小火箭极简配置（手动/自动 + 国内直连）
└── README.md
```

## config.example.yaml 是什么

一份「手动选一台 / 自动最快」的极简配置，四种分组：

- **🚀 节点选择**（select）：总开关，第一项「🌐 全局代理」、第二项「♻️ 自动选择」，往下每一台节点 = 手动固定
- **🌐 全局代理**（select）：内部指向「自动选择」，切到它 = 所有流量（含国内）都走代理
- **♻️ 自动选择**（url-test）：全部节点测速取最快，挂了自动换下一个
- **🔀 分流开关**（select）：国内流量默认直连，切到「全局代理」则国内也走代理

国内流量三层识别（银行域名 → geosite:cn → geolocation-cn → GEOIP,CN），其余全走你选的组。

## 怎么用

1. 下载 `config.example.yaml`
2. 把 `proxy-providers.all.url` 里的 `"在这里填你的订阅地址"` 改成你自己的节点订阅地址
3. 导入客户端（Clash Verge / v2rayN / Stash / 小火箭 等）

就这三步，其余不用动。

## shadowrocket.example.conf 是什么

给小火箭（Shadowrocket，iOS）用的极简配置，同样是「手动/自动」两种模式：

- **🚀 节点选择**（select）：第一项「♻️ 自动选择」= 自动模式，往下是订阅注入的节点 = 手动固定
- **♻️ 自动选择**（url-test）：全部节点测速取最快，挂了自动换下一个

国内流量走 ChinaMax 名单直连，被墙流量走 `ProxyGFWlist` 代理，其余兜底走代理。

**注意**：这份小火箭配置里，规则集引用的是公共开源仓库（blackmatrix7 / ACL4SSR / Aethersailor），
节点通过你的订阅自动注入（`use=true`），配置里不写死节点。

## 规则集

规则集直接指向 MetaCubeX 官方源（`meta-rules-dat`），社区持续更新，**无需自己维护**：

```
https://testingcf.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@meta/geo/geosite/cn.mrs
```

国内识别用的规则集（private / bank-cn / cn / geolocation-cn）都来自官方源，VPS 废了也不影响国内分流。
