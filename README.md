# 🍔 麦当劳 AI 助手（mcd-helper）

基于麦当劳官方 MCP 能力（`mcd-mcp` · streamable HTTP · `https://mcp.mcd.cn`）构建的 AI 技能，覆盖四个场景：

| 场景 | 能力 |
|---|---|
| 🥗 减脂配餐 | 按热量预算组合高蛋白低卡套餐，标注营养成分与避雷项 |
| 💰 优惠券省钱助手 | 查询实时优惠券，计算最优用券组合与节省金额 |
| 🍱 套餐推荐 | 按口味/预算/人数推荐 2–3 套组合，含券后价 |
| 🧾 点餐助手 | 订单确认、下单、支付链接、重付引导 |

## 项目结构

```
mcdonalds-ai-skill/
├── skill/mcd-helper/SKILL.md   # AI 技能主体（WorkBuddy Skill 格式）
├── config/mcp.example.json     # MCP 配置模板（Token 已脱敏为占位符）
└── .gitignore                  # 排除本地真实配置，防止 Token 泄漏
```

## 安装 MCP

1. 复制配置模板：

   ```bash
   cp config/mcp.example.json config/mcp.json
   ```

2. 将 `<YOUR_MCD_MCP_TOKEN>` 替换为你的真实 Token（获取方式：麦当劳 MCP 开放平台申请）。
3. 将 `mcd-mcp` 节点合并进 `~/.workbuddy/mcp.json`（或对应客户端的 MCP 配置文件）：

   ```json
   {
     "mcpServers": {
       "mcd-mcp": {
         "type": "streamablehttp",
         "url": "https://mcp.mcd.cn",
         "headers": {
           "Authorization": "Bearer <YOUR_MCD_MCP_TOKEN>"
         }
       }
     }
   }
   ```

4. 重启客户端 / 在连接器管理页对新 MCP 服务器点击「信任」即可激活。

## 安装技能

把 `skill/mcd-helper/` 整个目录复制到：

- WorkBuddy 用户级技能：`~/.workbuddy/skills/mcd-helper/`
- 或项目级技能：`<项目>/.workbuddy/skills/mcd-helper/`

## 安全说明

- 仓库中的 `config/mcp.example.json` 仅含占位符，**不含任何真实凭据**。
- 本地真实配置（`config/mcp.json` / `config/mcp.local.json`）已加入 `.gitignore`。
- 技能运行时会拒绝向用户展示或转述 Authorization Token。

## License

MIT
