# StallTCP1.3V1 节点订阅管理面板 (D1 数据库增强版)

**优先级顺序为：环境变量 (Env) > D1 数据库 > KV 空间 > 代码中的默认配置**

**这是一个基于 Cloudflare Workers / Snippets 的高级节点订阅管理与分发系统。**

它集成了 **自适应订阅生成**、**优选IP自动负载均衡**、**智能黑名单防御**、**Telegram 实时通知** 以及 **可视化的后台管理面板**。

> **核心特性：** 无需服务器，零成本部署，支持 **KV / D1 (SQLite) / R2** 持久化存储，自带毛玻璃 UI 后台。

---

## 📂 代码版本说明 (必读)

本项目包含两套代码，请根据您的部署方式选择：

*   **Worker / Pages 部署**：请使用 **`_worker.js`** 代码。
    *   *UI 特效：高级毛玻璃风格*
    *   *新增特性：支持 D1 数据库高速读写、强制会话登录验证*
*   **Snippets 部署**：请使用 **`snippets.js`** 代码。 【也支持worker/pages部署】
    *   *UI 特效：紫色渐变风格*

**如果项目对您有帮助，请给我点亮星星 Star 🌟 谢谢！**

---

## ✨ 功能特性

**✅ 完美支持 Cloudflare Workers**
**✅ 完美支持 Cloudflare Pages**
**✅ 完美支持 Cloudflare Snippets**

### 🆕 新增增强功能 (Worker版)
*   **🗄️ D1 数据库支持**：完美支持 Cloudflare D1 (SQLite)，日志记录更全，统计更准，且无 KV 的写入频率限制。
*   **🔐 强制安全登录**：采用**会话级**验证机制。关闭浏览器或标签页即自动退出登录，每次进入后台均需重新验证密码，极大提升安全性。
*   **🚫 增强型防刷**：基于数据库的洪水攻击检测，单 IP 短时间频繁请求自动拉黑。

### 核心功能详情
*   **🚀 自适应订阅**：自动识别客户端（Clash, Sing-box, v2rayNG 等），返回对应格式的配置。
*   **🌍 优选 IP 支持**：
    *   内置优选库，支持随机打乱负载均衡。
    *   支持单行多 IP 配置（逗号/分号分隔），灵活方便。
    *   支持远程 TXT/CSV 订阅源自动抓取更新。
*   **🛡️ 智能防御系统**：
    *   **自动拉黑**：检测到单 IP 频繁刷新订阅或访问网页（>5次），自动封禁并通知。
    *   **持久化黑名单**：支持绑定 Cloudflare KV 或 D1 数据库，黑名单永不丢失。
    *   **手动黑/白名单**：支持通过环境变量或后台面板手动管理 IP。
*   **🤖 Telegram 通知**：
    *   详细记录用户访问、订阅更新、检测站点击等行为。
    *   精准识别客户端类型与来源 IP。
*   **📊 后台管理面板**：
    *   **毛玻璃 UI**：美观的现代化界面，适配移动端。
    *   **黑名单管理**：在后台直接添加/删除黑名单 IP，实时生效。
    *   **用量统计**：集成 Cloudflare API，实时查看今日请求数消耗。
*   **🔐 安全机制**：
    *   支持动态 UUID（随时间自动变更）。
    *   支持自定义后台密码与订阅路径密码。

**界面预览：** worker全新界面/snippets界面
<img width="100%" alt="image" src="https://github.com/user-attachments/assets/e43db73f-4d8d-41a3-ab43-61555c8c984b" />
<img width="1920" height="918" alt="image" src="https://github.com/user-attachments/assets/609af76b-99ae-4fe6-ac08-1878ca34f369" />
<img width="1920" height="918" alt="image" src="https://github.com/user-attachments/assets/84bf305e-7072-403e-8389-628349a29e3f" />

---

## 🚀 部署指南一：Worker / Pages 代码版 (`_worker.js`)

**适用场景：Cloudflare Workers 或 Cloudflare Pages**

### 方式 A：Cloudflare Workers 部署 (最简单)
1.  登录 Cloudflare Dashboard。
2.  找到 **计算 (Workers & Pages)** -> **概述**。
3.  选择 **从 Hello World! 开始**。
    <img width="800" alt="image" src="https://github.com/user-attachments/assets/2b80a97b-ee57-42a8-be1a-8180254f54dc" />
4.  输入任意名称，点击 **部署**。
    <img width="800" alt="image" src="https://github.com/user-attachments/assets/b26217ed-d17c-465d-bcbd-b232ab5a4fd0" />
5.  在 Workers 列表找到刚部署的项目，点击 **编辑代码**。
    <img width="800" alt="image" src="https://github.com/user-attachments/assets/a7f0c75a-56c3-467b-a07f-d37cafb8dd6c" />
6.  **清空**原有代码，将项目中的 **`_worker.js`** 内容完整复制粘贴进去。
7.  点击右上角 **保存并部署**。

### 方式 B：Cloudflare Pages 部署
**注意：修改任何内容都需要重新上传一次代码**

1.  登录 Cloudflare -> **Workers 和 Pages**。
    <img width="600" alt="image" src="https://github.com/user-attachments/assets/75c41546-cc6a-4a2f-9fa5-3632f0d89104" />
2.  点击 **创建应用程序**。
    <img width="800" alt="image" src="https://github.com/user-attachments/assets/6ddd7c84-4a4f-4ddc-bd41-f2d550139999" />
3.  点击下方的 **Get started** 跳转到 Pages 界面。
    <img width="800" alt="image" src="https://github.com/user-attachments/assets/f5fdaa8d-d86a-471e-93de-9107db440443" />

#### (方法 1) GitHub 自动同步 (推荐)
1.  选择 **连接到 Git**。
    <img width="800" alt="image" src="https://github.com/user-attachments/assets/8932221a-6480-491d-baf9-a26fc67a852b" />
2.  选择你 Fork 的 GitHub 仓库。
    <img width="800" alt="image" src="https://github.com/user-attachments/assets/2518c4e5-8503-4b4c-80f9-6ca06dfb0df9" />
3.  **特别注意**：后续修改内容要在 GitHub 上的 `_worker.js` 进行修改，之后会自动同步到 Pages。
4.  点击 **开始设置**，然后 **保存并部署**。
    <img width="800" alt="image" src="https://github.com/user-attachments/assets/1c215f82-98fc-42d0-aed5-2bd032e3b859" />

#### (方法 2) 直接上传
1.  选择 **上传资产**。
    <img width="800" alt="image" src="https://github.com/user-attachments/assets/5f823410-7308-4425-9e77-a66646235e00" />
2.  输入项目名称，点击创建。
    <img width="800" alt="image" src="https://github.com/user-attachments/assets/c10dc676-a06a-4a6b-bc62-f24239f454b0" />
3.  上传包含 `_worker.js` 的 **Zip 压缩包** 或 **文件夹**。
    <img width="800" alt="image" src="https://github.com/user-attachments/assets/5dec9d85-9fcb-4b95-89c6-a7d8c57be661" />
4.  点击 **部署站点**。

---

## 🚀 部署指南二：Snippets 代码版 (`snippets.js`)

**适用场景：已有域名托管在 Cloudflare，想利用 Snippets 功能**

1.  进入 Cloudflare Dashboard，点击你的**域名**。
    <img width="800" alt="image" src="https://github.com/user-attachments/assets/2483c2b7-3bb2-4cac-bdd6-38f8b31f4329" />
2.  在左侧菜单找到 **规则 (Rules)** -> **Snippets**，点击 **创建片段**。
    <img width="800" alt="image" src="https://github.com/user-attachments/assets/9059a47d-77da-4ba4-82cc-03e8a8638c0f" />
3.  输入片段名称。
4.  将项目中的 **`snippets.js`** 内容完整复制粘贴进去。
    <img width="800" alt="image" src="https://github.com/user-attachments/assets/f163e9ef-989b-4645-8ebc-eadf755f4b23" />
5.  **设置触发规则**：
    *   选择 **自定义规则**。
    *   字段：`主机名 (Hostname)`
    *   运算符：`等于 (equals)`
    *   值：你的子域名 (例如 `sub.yourdomain.com`)
    <img width="800" alt="image" src="https://github.com/user-attachments/assets/1f858efe-a6ce-4bf6-8d62-0bfc462ef2b3" />
6.  点击 **创建片段** 保存。
7.  **配置 DNS (重要)**：
    *   前往 **DNS** 设置页，添加一条 **A 记录**。
    *   **名称**：填写上面设置的子域名 (例如 `sub`)。
    *   **IPv4 地址**：`192.0.2.1` (保留地址，仅作占位用)。
    *   **代理状态**：必须开启 **小黄云 (Proxied)**。
    <img width="600" alt="image" src="https://github.com/user-attachments/assets/f88ad346-30aa-41ef-9f7c-deb2453afbfe" />

---

## ⚡️ 进阶配置：D1 数据库 (推荐 - 性能更强)

**本版本不仅支持 KV，还支持 Cloudflare D1 (SQLite) 数据库。相比 KV，D1 拥有更快的写入速度和更大的容量，且不会出现 KV 的写入频率限制错误。**

1.  **创建数据库**：
    *   在 Cloudflare 左侧菜单选择 **Workers & Pages** -> **D1**。
    *   点击 **创建数据库**，命名为 `sub_db` (或其他你喜欢的名字)。

2.  **初始化表结构 (必做)**：
    *   进入刚才创建的数据库，点击 **控制台 (Console)** 标签。
    *   复制以下 SQL 代码粘贴到控制台并点击 **Execute (执行)**：
    ```sql
    CREATE TABLE IF NOT EXISTS config (key TEXT PRIMARY KEY, value TEXT);
    CREATE TABLE IF NOT EXISTS logs (id INTEGER PRIMARY KEY AUTOINCREMENT, time TEXT, ip TEXT, region TEXT, action TEXT);
    CREATE TABLE IF NOT EXISTS stats (date TEXT PRIMARY KEY, count INTEGER DEFAULT 0);
    CREATE TABLE IF NOT EXISTS flood (ip TEXT PRIMARY KEY, count INTEGER DEFAULT 0, updated_at INTEGER);
    CREATE TABLE IF NOT EXISTS bans (ip TEXT PRIMARY KEY, is_banned INTEGER DEFAULT 0);
    ```

3.  **绑定变量**：
    *   回到你的 Worker 项目设置。
    *   点击 **设置** -> **变量** -> **D1 数据库绑定**。
    *   变量名称：**`DB`** (必须大写，不能改名)。
    *   选择刚才创建的数据库。
    *   **保存并部署**。

---

## 💾 兼容模式：绑定 KV (可选)

**如果您不想配置 D1，使用的是 worker.js 版本，请使用 KV。代码会自动识别。**

1.  在 Cloudflare 左侧菜单选择 **Workers & Pages** -> **KV**。
2.  点击 **创建命名空间 (Create a Namespace)**，命名为 `BLACKLIST`（或任意名称）。
3.  回到你的 Worker/Pages/Snippet 项目设置页：
    *   **Workers/Pages**：`设置` -> `变量` -> `KV 命名空间绑定`。
4.  点击 **添加绑定**：
    *   **变量名称 (Variable name)**: `LH` (⚠️必须填这个，不能改)
    *   **KV 命名空间**: 选择你刚才创建的空间。
5.  **保存并重新部署**。

---

## ⚙️ 环境变量配置 (Variables)

您可以直接在 Cloudflare 项目的 `Settings` -> `Variables` 中设置以下变量。
> **注意**：如果未设置环境变量，系统将使用代码中内置的默认配置（兜底）。**为了安全，强烈建议设置密码相关的变量！**

### 🧱 基础配置 (Basic Config)

| 变量名 | 说明 | 示例 / 默认值 |
| :--- | :--- | :--- |
| `UUID` | **主 UUID** (用户ID)，客户端连接凭证 | `06b65903-406d-4a41-8463-6fd5c0ee7798` |
| `WEB_PASSWORD` | **后台登录密码** (如果不填则无法登录或默认空) | `yourpassword` |
| `SUB_PASSWORD` | **订阅路径密码** (访问 `https://域名/密码` 获取订阅) | `my-secret-sub` |
| `PROXYIP` | **默认优选域名/IP** (节点连接地址) | `cf.090227.xyz` |
| `SUB_DOMAIN` | **真实订阅源** (上游优选订阅生成器地址) | `sub.cmliussss.net` |
| `PS` | **节点备注** (显示在节点名称后) | `【专线】` |
| `SUBAPI` | **订阅转换后端** (用于 Sing-box/Clash 转换) | `https://subapi.cmliussss.net` |

### 🌍 节点来源配置 (Node Sources)

| 变量名 | 说明 | 格式说明 |
| :--- | :--- | :--- |
| `ADD` | **本地优选 IP 列表** | 支持**换行**、**逗号**分隔。<br>例：`1.1.1.1:443#美国, 2.2.2.2#香港` |
| `ADDAPI` | **远程 TXT 优选列表** | 填入 URL，格式同上 (一行一个 IP) |
| `ADDCSV` | **远程 CSV 优选列表** | 填入 URL，支持高级节点信息导入 |

### 🛡️ 安全与通知 (Security & Notify)

| 变量名 | 说明 | 示例 / 默认值 |
| :--- | :--- | :--- |
| `TG_BOT_TOKEN` | **Telegram 机器人 Token** (用于发送通知) | `123456:ABC-DEF...` |
| `TG_CHAT_ID` | **Telegram 用户 ID** (接收通知的账号) | `123456789` |
| `KEY` | **动态 UUID 开关** | 填 `false` 关闭；填任意字符串 (如 `secret`) 开启 |
| `UUID_REFRESH` | **动态 UUID 刷新间隔** (单位：秒) | `86400` (默认 1 天) |
| `BJ_IP` | **静态黑名单 IP** (永久禁止访问) | `1.1.1.1, 2.2.2.2` (英文逗号分隔) |
| `WL_IP` | **静态白名单 IP** (免检，视为管理员) | `210.61.97.241` (英文逗号分隔) |

### 💾 存储绑定变量名 (Bindings)

> **注意**：变量名必须完全一致。优先检测 `DB`，若无则使用 `LH`。

| 变量名 | 类型 | 推荐度 | 用途 |
| :--- | :--- | :--- | :--- |
| **`DB`** | **D1** | **⭐⭐⭐⭐⭐** | **D1 数据库绑定**。高性能存储日志、黑名单、统计数据。 |
| **`LH`** | **KV** | **⭐⭐⭐** | **KV 命名空间绑定**。兼容旧版存储。如果未绑定 D1，系统将自动回退使用 KV。 |
| `R2` | R2 | 可选 | 预留接口，暂未启用 |

---

## 🖥️ 后台管理使用说明

访问 `https://你的域名 直接访问域名进入管理后台。

或者https://你的域名/路径或者密码 [SUB_PASSWORD] 这个密码 可以直接查看节点信息并返回base64节点信息

*   **🔒 强制安全登录**：
    *   本版本启用了**会话级强制验证**。
    *   关闭浏览器标签页或刷新页面（视缓存策略而定）会自动退出登录。
    *   下次访问必须重新输入密码，防止他人通过历史记录进入后台。
*   **黑名单管理**：
    *   在面板中可以直接输入 IP 添加到黑名单。
    *   列表实时从 D1/KV 读取，支持一键删除。
    *   被拉黑的 IP 将无法访问订阅和网页（直接返回 403）。
*   **用量统计**：
    *   集成 Cloudflare API，实时查看今日请求数消耗。
    *   *注：若使用 D1，后台会优先显示 D1 存储的今日请求统计。*
*   **快捷操作**：
    *   支持一键复制订阅链接、Clash/Sing-box 快速导入。
    *   集成 ProxyIP 连通性检测工具。

> ⚠️ **注意事项**
>
> - **关于默认密码**：代码中默认 `WEB_PASSWORD` 和 `SUB_PASSWORD` 为空。为了安全，**请务必在环境变量中设置这两个值**。
> - **自动拉黑机制**：默认策略为 **5次**。同一个 IP 在短时间内刷新网页或订阅超过 5 次，将自动加入D1数据库/KV黑名单。
> - **优选 IP 格式**：`ADD` 变量支持极其灵活的格式，你可以直接粘贴多行，或者用逗号分隔，代码会自动解析。例如：`1.1.1.1#US, 2.2.2.2:8443#HK`

---

## 🙏 特别感谢与致谢

**特别感谢天诚修复的所有 Bug 与新增功能：**
*   ❇️ 修复了 Cloudflare 网站不能访问的问题。
*   ❇️ 新增加了机场三字码的适配。
*   ❇️ 新增负载均衡轮询。
*   ❇️ 新增解锁 Emby 播放器。
*   ❇️ 新增了韩国节点适配。
*   ❇️ Trojan/Vless 订阅器内置 CSV 文件优化识别功能。

**相关支持与链接：**
*   **源代码作者**：[Alexandre_Kojeve](https://t.me/Alexandre_Kojeve) (致敬原版 stallTCP1.3)
*   **后台作者**：[ym94203](https://t.me/ym94203)
*   **ProxyIP 支持**：[COMLiang](https://t.me/COMLiang)
*   **Telegram 交流群**：[zyssadmin](https://t.me/zyssadmin)
*   **Cloudflare Docs**：[Support](https://developers.cloudflare.com/)

---

## ⚖️ 免责声明

**本项目仅供技术交流与学习使用，请勿用于非法用途。使用本程序产生的任何后果由使用者自行承担。**
