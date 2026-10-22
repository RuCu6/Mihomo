Loon Rules -> Nikki (mihomo) 转换说明
=====================================
来源: GitHub RuCu6/Loon 仓库 Rules/ (commit 14fae78)
文件: 14 个 *.list, mihomo classical 文本格式 (behavior: classical, format: text)
      另附 nikki-rule-providers.yaml 接入片段

转换内容 (原 2229 条 -> 2208 条):
1. 去掉每条规则逗号后的空格: "DOMAIN-SUFFIX, a.com" -> "DOMAIN-SUFFIX,a.com"
   (mihomo classical 格式不带空格)
2. IP6-CIDR -> IP-CIDR6 (Global 5 条), 并补 no-resolve
3. IP-CIDR / IP-CIDR6 / IP-ASN 缺 no-resolve 的补齐 (Global 18 条),
   保证按目标 IP 直接匹配, 不额外触发 DNS 解析
4. GEOIP,cn -> GEOIP,CN (China 1 条, mihomo 国家码须大写)
5. Spotify 里 "DOMAIN-KEYWORD,-spotify-,Spotify" 末尾的 Spotify 是
   残留的策略名, rule-provider 文件内不能带策略, 已去掉;
   策略在引用处 (RULE-SET 行) 决定
6. PornAds 内 21 条完全重复的规则已去重 (原文件多段引用同一批域名)
7. README.lsr 不是规则文件 (只有 4 条引用网址, 0 条规则), 未转换

原样保留:
- WeChat 的 USER-AGENT,MicroMessenger* / WeChat* (mihomo 支持 USER-AGENT)
- 注释行 (# 开头) 全部保留

策略对应 (按 Loon.lcf 的 [Remote Rule]):
PornAds=REJECT, Global=代理, LAN/Apple/Speedtest/WeChat/China=DIRECT
其余 7 个文件 Loon 配置里未引用, yaml 里默认注释, 策略给了建议值。
