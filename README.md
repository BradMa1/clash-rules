# clash-rules

自建节点用的 clash 配置模板 + 规则集，经 jsdelivr CDN 分发，不依赖任何固定 VPS。

## 目录

```
clash-rules/
├── config.example.yaml   # 极简配置模板（2 个组：手动/自动 + 国内直连）
├── README.md
└── geosite/              # 规则集（.mrs，供 config 的 rule-providers 拉取）
    ├── private.mrs
    ├── category-bank-cn.mrs
    ├── cn.mrs
    └── geolocation-cn.mrs
```

## config.example.yaml 是什么

一份「只有两种模式」的极简配置：

- **🚀 节点选择**（select）：第一项「♻️ 自动选择」= 自动模式，往下每一台节点 = 手动固定
- **♻️ 自动选择**（url-test）：全部节点测速取最快，挂了自动换下一个

国内流量三层直连（银行域名 → geosite:cn → geolocation-cn → GEOIP,CN），其余全走你选的组。

## 怎么用

1. 下载 `config.example.yaml`
2. 把 `proxy-providers.all.url` 里的 `"在这里填你的订阅地址"` 改成你自己的节点订阅地址
3. （可选）把 `fake-ip-filter` 里的 `+.example.com` 换成你自己的订阅/面板域名
4. 导入客户端（Clash Verge / v2rayN / Stash 等）

## 规则集

规则集托管在本仓库 `geosite/` 目录，客户端通过 jsdelivr 拉取：

```
https://cdn.jsdelivr.net/gh/BradMa1/clash-rules@main/geosite/cn.mrs
```

国内识别用的规则集（private / bank-cn / cn / geolocation-cn）都在这里，VPS 废了也不影响国内分流。
