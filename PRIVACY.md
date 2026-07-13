# RouteLens 隐私政策

生效日期：2026 年 7 月 13 日

> 发布前请将文末的联系方式替换为开发者的真实联系方式，并将本政策发布在公开 HTTPS 网页。

RouteLens 的单一用途是：在用户主动点击扩展时，检查当前站点路由下的出口 IP、IP 风险信号、浏览器连接对端和公共 DNS 解析 IP。

## 处理的数据

- 当前站点域名：在本机内存中用于同域检测和显示，并发送给 Cloudflare 公共 DNS 以查询公开 A 记录；不保存为浏览历史，不发送给 IP 情报服务。
- 公共 IP 地址：基础检测会通过 HTTPS 请求 ipify，ipify 能够观测到该请求的来源 IP。
- IP 情报查询：RouteLens 会通过 HTTPS 将当前检测到的 IP 地址优先发送给 FFraud；查询失败时并行查询 ipquery.io 和 ipwho.is。三者均无需用户账号或 API Key；ipwho.is 仅作为网络归属保底来源。
- 本地纯净分：由扩展根据情报服务返回的风险标记在本机内存中计算，不发送给开发者，也不保存。
- 连接对端：用户点击扩展后，RouteLens 会向当前站点请求 `/favicon.ico`，读取 Chrome 连接的对端 IP。使用本机代理时，该地址可能是 `127.0.0.1`。
- 公共 DNS IP：当前站点域名会通过 HTTPS 发送给 Cloudflare DNS，以查询公开 A 记录。

## 第三方服务

- ipify：用于检测公共出口 IP。详见 [ipify 隐私政策](https://www.ipify.org/privacy-policy/)。
- FFraud：首选的开放 IP 风险情报服务。详见 [FFraud 网站](https://ffraud.com/)。
- ipquery.io：FFraud 查询失败时使用的 IP 地理位置、归属和风险标记服务。详见 [ipquery.io 隐私政策](https://ipquery.io/privacy)。
- ipwho.is：其他情报域名不可达时提供网络归属保底结果。详见 [ipwho.is 隐私政策](https://ipwhois.io/privacy-policy)。
- Cloudflare DNS：用于查询当前站点域名的公开 DNS A 记录。详见 [Cloudflare 隐私政策](https://www.cloudflare.com/privacypolicy/)。

RouteLens 不将数据用于广告，不出售数据，不使用分析或追踪 SDK，不允许人工阅读用户数据。

## 保留与删除

RouteLens 不保存检测历史或 API Key。第三方服务对请求日志的保留受各自隐私政策约束。

## 权限

- `activeTab`：仅在用户点击扩展时读取当前标签页域名并发起同域 IP 探测。
- `scripting`：在用户主动点击扩展后，向当前标签页注入一次同域站点连接探测；不读取或修改页面内容。
- `webRequest`：读取上述一次性同域探测所连接的对端 IP。
- `api64.ipify.org` 主机权限：请求公共出口 IP。
- `api.ffraud.com` 主机权限：无需 Key 查询已检测 IP 的开放风险情报。
- `api.ipquery.io` 主机权限：首选情报源失败时查询地理位置、网络归属和风险标记。
- `ipwho.is` 主机权限：首选情报源失败时提供网络归属保底结果。
- `cloudflare-dns.com` 主机权限：查询当前站点域名的公开 DNS A 记录。

## 政策变更

如果数据处理方式发生实质变更，开发者将更新本政策、Chrome 网上应用店数据声明和扩展内说明，并在必要时重新获得用户同意。

## 联系方式

开发者：`[请填写开发者名称]`  
联系邮箱：`[请填写支持邮箱]`
