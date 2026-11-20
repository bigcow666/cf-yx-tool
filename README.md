## Cloudflare Workers 环境变量说明（全部选 Text 明文）

| 变量名 | 是否必填 | 默认值 | 说明 | 填写示例 |
| :--- | :---: | :--- | :--- | :--- |
| **`NODES`** | 必填 | 无 | 原始节点链接，**一行一个**（原链接参数全部保留） | `vless://uuid@域名:443?encryption=...#备注` |
| **`SUB_PATH`** | 可选 | `sub` | 自定义订阅路径前缀（防扫描） | `my888` |
| **`BEST_IPS`** | 可选 | 无 | 自定义优选域名/IP 列表，**一行一个**，优先级最高（支持端口与备注） | `saas.sin.fan:443#优选1`<br>`104.16.1.1:2053#直连IP` |
| **`IP_URL`** | 可选 | 内置 `defaultIPURL` | 远程优选列表地址；不填默认拉取内置 URL；填 `none` 或 `off` 则关闭远程拉取 | `https://example.com/bestip.txt` 或 `none` |

## 订阅与安全规则

- **订阅地址格式**：`https://你的Worker域名/SUB_PATH/原节点UUID`
- **合并与去重顺序**：`BEST_IPS` > 内置 `directDomains` > 远程 `IP_URL`（按 `host:port` 自动去重，保留先出现的备注）
- **访问限制**：已拦截普通浏览器（直接访问主域名、路径错误、UUID 错误或浏览器打开均返回空 `404`），仅放行代理客户端拉取 Base64 订阅。
