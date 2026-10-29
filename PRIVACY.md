# RouteLens 隐私政策

生效日期：2026 年 10 月 29 日

RouteLens 的单一用途是：检查当前站点路由下的出口 IP、出口国家、IP 风险信号、浏览器连接对端和公共 DNS 解析 IP；用户还可主动监控指定站点的出口变化。

## 处理的数据

- 当前站点域名：在本机用于同域检测和显示；用户打开弹窗时还会发送给 Cloudflare 公共 DNS 查询公开 A 记录。自动检测默认关闭，只有用户授权后才会在切换或加载网页时运行。当前标签页域名会随最近结果临时保存在 `chrome.storage.session`；用户主动添加的监控域名则保存在本机 `chrome.storage.local`。RouteLens 不持续记录所有访问过的网站，也不将域名发送给 IP 情报服务。
- 公共 IP 地址：基础检测会通过 HTTPS 请求 ipify，ipify 能够观测到该请求的来源 IP。
- IP 情报查询：RouteLens 会通过 HTTPS 将当前检测到的 IP 地址优先发送给 FFraud；查询失败时并行查询 ipquery.io 和 ipwho.is。三者均无需用户账号或 API Key；ipwho.is 仅作为网络归属保底来源。
- 本地纯净分：由扩展根据情报服务返回的风险标记在本机内存中计算，不发送给开发者，也不保存。
- 连接对端：用户点击扩展后，RouteLens 会向当前站点请求 `/favicon.ico`，读取 Chrome 连接的对端 IP。使用本机代理时，该地址可能是 `127.0.0.1`。
- 公共 DNS IP：当前站点域名会通过 HTTPS 发送给 Cloudflare DNS，以查询公开 A 记录。
- 目标站点 IP：打开弹窗后，RouteLens 会选择 Chrome 返回的公开连接对端 IP；若连接对端为本机代理或私有地址，则选择一个公共 DNS A 记录，并发送给 IP 情报服务查询该站点 IP 的国家或地区。目标站点 IP 是公开服务器地址，不会保存。
- 自动检测设置：本机保存用户是否开启自动检测的布尔值。
- 会话缓存：为避免重复打开弹窗时重新等待，RouteLens 通过内存型 `chrome.storage.session` 按标签页临时保存最近一次完整检测结果。缓存最长保留 12 小时，站点变化时不会跨域复用，关闭标签页或浏览器后清除，不会同步或形成历史列表。
- 指定站点监控：用户可主动添加最多 5 个域名和预期国家。只有开启自动检测并访问这些站点时，扩展才在本机 `chrome.storage.local` 保存该站点的出口 IP、国家、测量方式和检测时间。最多保留 30 天、500 条变化记录；用户可单独移除站点或清空历史。监控历史不上传给 AiOmniaHub，也不跨设备同步。仅本站同域回显的实测结果会触发预期国家偏离提醒，公共探针估算不会。

## 第三方服务

- ipify：用于检测公共出口 IP。详见 [ipify 隐私政策](https://www.ipify.org/privacy-policy/)。
- FFraud：首选的开放 IP 风险情报服务。详见 [FFraud 网站](https://ffraud.com/)。
- ipquery.io：FFraud 查询失败时使用的 IP 地理位置、归属和风险标记服务。详见 [ipquery.io 隐私政策](https://ipquery.io/privacy)。
- ipwho.is：其他情报域名不可达时提供网络归属保底结果。详见 [ipwho.is 隐私政策](https://ipwhois.io/privacy-policy)。
- Cloudflare DNS：用于查询当前站点域名的公开 DNS A 记录。详见 [Cloudflare 隐私政策](https://www.cloudflare.com/privacypolicy/)。

RouteLens 不将数据用于广告，不出售数据，不使用分析或追踪 SDK，不允许人工阅读用户数据。

RouteLens 对从 Chrome API 获得的信息的使用遵守 Chrome 网上应用店用户数据政策，包括 Limited Use（有限使用）要求。

## 保留与删除

RouteLens 不要求账号、密码、邮箱、付款信息或 API Key。用户主动启用的指定站点监控历史在本机保留最多 30 天、500 条，可随时在监控页清空；到期记录会在下次打开监控页或记录新结果时清理。关闭标签页或浏览器会清除对应会话缓存；卸载扩展会清除本机扩展存储。第三方服务对请求日志的保留受各自隐私政策约束。

## 权限

- `activeTab`：仅在用户点击扩展时读取当前标签页域名并发起同域 IP 探测。
- `scripting`：在用户主动点击扩展后，向当前标签页注入一次同域站点连接探测；不读取或修改页面内容。
- `webRequest`：读取上述一次性同域探测所连接的对端 IP。
- `storage`：通过 `chrome.storage.local` 保存自动检测开关、用户指定的监控域名和本机变化历史；通过 `chrome.storage.session` 临时缓存当前标签页最近一次检测结果。数据不跨设备同步。
- 可选 HTTP/HTTPS 站点权限：仅在用户主动开启自动检测时请求，用于在切换或加载普通网页后执行同域 IP 回显检测并更新工具栏国家图标。关闭自动检测会撤销此权限。
- `api64.ipify.org` 主机权限：请求公共出口 IP。
- `api.ffraud.com` 主机权限：无需 Key 查询已检测 IP 的开放风险情报。
- `api.ipquery.io` 主机权限：首选情报源失败时查询地理位置、网络归属和风险标记。
- `ipwho.is` 主机权限：首选情报源失败时提供网络归属保底结果。
- `cloudflare-dns.com` 主机权限：查询当前站点域名的公开 DNS A 记录。

## 政策变更

如果数据处理方式发生实质变更，开发者将更新本政策、Chrome 网上应用店数据声明和扩展内说明，并在必要时重新获得用户同意。

## 联系方式

开发者：Felix Zou  
联系邮箱：support@aiomniahub.com

