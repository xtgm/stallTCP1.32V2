# StallTCP1.3V1 节点订阅管理面板 (增强版)

**这是一个基于 Cloudflare Workers / Snippets 的高级节点订阅管理与分发系统。**

**它集成了 自适应订阅生成、优选IP自动负载均衡、智能黑名单防御、Telegram 实时通知 以及 可视化的后台管理面板。**

# 以下是两套代码方法部署

--------------------------------------

**snippets部署请看  snippets.js代码**

**worker部署请看  _worker.js代码**

--------------------------------------------

**核心特性： 无需服务器，零成本部署，支持 KV/D1/R2 持久化存储，自带毛玻璃 UI 后台。**

# 双UI特效

**snippets为紫色渐变UI** 

 **worker为毛玻璃特效**

**如果项目对您有帮助。请给我点亮星星star 谢谢**

**源代码来源于Alexandre_Kojeve的stallTCP1.3**

**特别说明 我只是完善了html后台管理页面**

**✅ 完美支持 Cloudflare Workers**  
**✅ 完美支持 Cloudflare Pages**  
**✅ 完美支持 Cloudflare snippets**  



**集成了 Web 管理后台、订阅转换.**

**优选 IP 自动解析（支持 .netlib 异步解析）以及 Clash/Sing-box 配置生成功能。**

**修复全平台所有兼容性问题 修复ios系统shadowrocket以及quantumult x兼容性问题**

<img width="1905" height="919" alt="image" src="https://github.com/user-attachments/assets/e43db73f-4d8d-41a3-ab43-61555c8c984b" />

-----------------------------------------------------------------------------------------------------------------

⚠️ 注意事项

> - 关于默认密码：代码中默认 WEB_PASSWORD 和 SUB_PASSWORD 为空。为了安全，请务必在环境变量中设置这两个值。
> - 自动拉黑机制：默认策略为 5次。同一个 IP 在短时间内刷新网页或订阅超过 5 次，将自动加入内存/KV黑名单。
> - 优选 IP 格式：ADD 变量支持极其灵活的格式，你可以直接粘贴多行，或者用逗号分隔，代码会自动解析。
> - 例如： 1.1.1.1#US, 2.2.2.2:8443#HK


------------------------------------------------------------------------------------------------------------------

# 🖥️ 后台管理使用说明
- 访问 https://你的域名/login 进入管理后台。

- 黑名单管理：
- 在面板中可以直接输入 IP 添加到黑名单。
- 列表实时从 KV 读取，支持一键删除。
- 被拉黑的 IP 将无法访问订阅和网页（直接返回 403）。
- 
# - 用量统计：
- 点击 "📊 统计设置"。
- 输入 Cloudflare 的 Account ID、Email 和 Global API Key。
- 点击 "可用性验证" 测试配置，成功后点击 "保存"。
- 保存后，每次进入后台都会自动显示当天的 Workers 请求数使用情况。

# 快捷操作：
- 支持一键复制订阅链接、Clash/Sing-box 快速导入。
- 集成 ProxyIP 连通性检测工具。


------------------------------------------------------------------------------------------------------------------







# ⚙️ 环境变量配置 (Variables) --worker变量参数参考
**您可以在 Cloudflare 后台 Settings -> Variables 中添加以下环境变量来覆盖默认配置。
如果不设置，系统将使用代码中默认的兜底配置。**

🧱 基础配置
变量名	说明	示例 / 默认值
UUID	你的主 UUID (用户ID)	06b65903-406d-4a41-8463-6fd5c0ee7798
WEB_PASSWORD	后台管理面板登录密码	yourpassword (不填则无密码/默认空)
SUB_PASSWORD	订阅路径密码 (隐藏订阅地址)	my-secret-sub (访问 /my-secret-sub 获取订阅)
PROXYIP	默认连接的优选域名/IP	cf.090227.xyz
SUB_DOMAIN	真实上游订阅源地址	sub.cmliussss.net
PS	节点名称备注/后缀	【专线】
SUBAPI	订阅转换后端地址	https://subapi.cmliussss.net

🌍 节点来源 (支持多行/逗号分隔)
变量名	说明	格式示例
ADD	本地优选 IP 列表	1.1.1.1:443#美国, 2.2.2.2#香港 (支持换行)
ADDAPI	远程 TXT 优选列表 API	https://example.com/ip.txt
ADDCSV	远程 CSV 优选列表 API	https://example.com/ip.csv

🛡️ 安全与通知
变量名	说明	示例
TG_BOT_TOKEN	Telegram 机器人 Token	123456:ABC-DEF...
TG_CHAT_ID	接收通知的 TG 用户 ID	123456789
KEY	动态 UUID 开关/密钥	填 false 关闭；填任意字符串开启
UUID_REFRESH	动态 UUID 刷新间隔 (秒)	86400 (默认1天)
BJ_IP	静态黑名单 IP 列表	1.1.1.1,2.2.2.2 (英文逗号分隔)
WL_IP	静态白名单 IP 列表	210.61.97.241 (免检 IP)

💾 存储绑定变量名 (代码中已固定)
变量名	类型	用途
LH	KV	(推荐) 黑名单持久化、配置保存
DR1	D1	(可选) 数据库备份存储
RG2	R2	(可选) 对象存储备份



-----------------------------------------------------------------------------------------------------------------

# 特别感谢天诚修复的所有bug功能

❇️修复了cloudflare网站不能访问的问题                                                                                                                     

❇️新增加了机场三字码的适配                                                                                                                       

❇️新增负载均衡轮询

❇️新增解锁Emby播放器

❇️新增了韩国节点适配

❇️Tojan订阅器内置CSV文件优化识别功能                                                                                          

❇️Vless订阅器内置CSV文件优化识别功能



------------------------------------------------------------------------------------------------------------------



## 📞 支持
- **源代码作者** ：https://t.me/Alexandre_Kojeve
- **proxyip支持** ：https://t.me/COMLiang
- **Telegram群组**: https://t.me/zyssadmin
- **telegram作者**：https://t.me/ym94203
- **Cloudflare Docs支持**: https://developers.cloudflare.com/

 🙏致敬原版作者：  Alexandre_Kojeve

 ⚠️ 后台作者：    ym94203
 
 👥 交流群组       zyssadmin 
 
 🤖  问题反馈/ 天诚技术交流群


------------------------------------------------------------------------------------------------------------------

## ⚙️ 配置说明 (Configuration)

在 `snippets.js` 代码的前几行，你需要根据需求修改以下变量：

## 🟣 用户配置区域
// =============================================================================

const UUID = "你的UUID";                 // 必填：建议使用 UUID Generator 生成

const WEB_PASSWORD = "你的后台密码";       // 必填：访问网页后台的密码

const SUB_PASSWORD = "你的订阅密码";             // 选填：快速订阅路径，访问 https://域名/123 即可

const DEFAULT_PROXY_IP = "tw.sni2025.netlib.re"; // 默认优选 IP 或域名

const DEFAULT_SUB_DOMAIN = "sub.cmliussss.net";  // 真实订阅源（用于聚合）


-----------------------------------------------------------------------------------------------------------------



-----------------------------------------------------------------------------------------------------------------


## ✨ 主要功能 【snippets】

- **🚀 VLESS 协议支持**：基于 `cloudflare:sockets`，实现高性能代理。
- **🛡️ 专属管理后台**：内置 Web 界面，可查看配置、复制订阅、检测 IP。
- **🔄 订阅聚合与转换**：支持抓取远程订阅源，并自动替换为 Worker 的节点信息。
- **⚡ 优选 IP 增强**：
  - 内置常用优选 IP 列表。 可自行修改自定义优选IP
  - **特色功能**：支持 `.netlib` 域名的异步 DoH 解析，自动获取动态优选 IP。
- **🔗 多客户端支持**：自动识别 User-Agent，为 Clash、Meta、Stash 等客户端生成专属配置。
- **🔐 安全认证**：支持自定义 UUID 和后台管理密码。

-----------------------------------------------------------------------------------------------------------------

-----------------------------------------------------------------------------------------------------------------

## ✨ 主要功能 【worker】

**🚀 自适应订阅**：自动识别客户端（Clash, Sing-box, v2rayNG 等），返回对应格式的配置。
**🌍 优选IP支持**：
**内置优选库，支持随机打乱负载均衡。
支持单行多IP配置（逗号/分号分隔），灵活方便。
支持远程 TXT/CSV 订阅源自动抓取更新。**
**🛡️ 智能防御系统**：
**自动拉黑：检测到单 IP 频繁刷新订阅或访问网页（>5次），自动封禁并通知。**
**持久化黑名单：支持绑定 Cloudflare KV，黑名单永不丢失。**
**手动黑/白名单：支持通过环境变量或后台面板手动管理 IP。**
**🤖 Telegram 通知**：
**详细记录用户访问、订阅更新、检测站点击等行为。
精准识别客户端类型与来源 IP。**
**📊 后台管理面板**：
**毛玻璃 UI：美观的现代化界面，适配移动端。**
**黑名单管理：在后台直接添加/删除黑名单 IP，实时生效。**
**用量统计：集成 Cloudflare API，实时查看今日请求数消耗。**
**🔐 安全机制**：
**支持动态 UUID（随时间自动变更）。**
**支持自定义后台密码与订阅路径密码。**


------------------------------------------------------------------------



------------------------------------------------------------------------

# 🛠️ 部署指南
1. 部署代码
登录 Cloudflare Dashboard。
创建一个新的 Worker
复制本项目 _worker.js 的完整代码并粘贴。
点击 保存并部署。

# 绑定 KV (强烈推荐)
**为了实现黑名单永久保存和后台配置记忆，请务必绑定 KV：**
**在 Cloudflare 左侧菜单选择 Workers & Pages -> KV。**
**点击 Create a Namespace，命名为 BLACKLIST（或任意名称）。**
**回到你的 Worker/Snippet 设置页 -> Settings -> Variables -> KV Namespace Bindings。**
**点击 Add binding：**
**Variable name: LH (⚠️必须填这个)**
**KV Namespace: 选择你刚才创建的空间。**
**保存并重新部署。**


-----------------------------------------------------------------------------

**【下方为snippets代码部署】**

## 🚀 快速开始

--- **worker部署**（小白最优选择）
部署 CF Worker：

登录你的cloudflare
找到计算和AI里的Workers 和 Pages：
选择从 Hello World! 开始：

<img width="1264" height="602" alt="image" src="https://github.com/user-attachments/assets/2b80a97b-ee57-42a8-be1a-8180254f54dc" />


输入任意的work名称之后点击部署即可

<img width="1645" height="806" alt="image" src="https://github.com/user-attachments/assets/b26217ed-d17c-465d-bcbd-b232ab5a4fd0" />


然后在cloudflare的Workers 和 Pages里面 找到你部署好的work项目 以我的项目为例： 点击编辑代码

<img width="1646" height="128" alt="image" src="https://github.com/user-attachments/assets/a7f0c75a-56c3-467b-a07f-d37cafb8dd6c" />


将 worker.js 的内容粘贴到 Worker 编辑器中并完成部署



**到这里worker部署就结束了**



---------------------------------------------------------------------

 # pages部署

**1.上传到 Cloudflare Pages** 【因为cloudflare改了UI 所以全新的方法】 

**特别注意 修改的内容要在github上的  worker.js  进行修改之后会同步cloudflare pages项目**

1.登录 Cloudflare  

找到计算AI-找到worker和pages
<img width="414" height="193" alt="image" src="https://github.com/user-attachments/assets/75c41546-cc6a-4a2f-9fa5-3632f0d89104" />
点击创建应用程序
<img width="1494" height="188" alt="image" src="https://github.com/user-attachments/assets/6ddd7c84-4a4f-4ddc-bd41-f2d550139999" />
点击下方的Get started 跳转到pages界面
<img width="1294" height="601" alt="image" src="https://github.com/user-attachments/assets/f5fdaa8d-d86a-471e-93de-9107db440443" />
选择第一个github 
<img width="1281" height="475" alt="image" src="https://github.com/user-attachments/assets/8932221a-6480-491d-baf9-a26fc67a852b" />
选择好的绑定好的github账号 

如果没有绑定你需要自己绑定 

然后选择好你fork的项目
<img width="1318" height="606" alt="image" src="https://github.com/user-attachments/assets/2518c4e5-8503-4b4c-80f9-6ca06dfb0df9" />

点击开始设置

写好项目名称【自己写】

写好项目名称之后 点击保存并部署

<img width="1113" height="870" alt="image" src="https://github.com/user-attachments/assets/1c215f82-98fc-42d0-aed5-2bd032e3b859" />

**这样pages github上传部署方法就完成了**

----------------------------------------------------------------------------------------------------------------------------------

**2.pages 上传方法** 

**【注意 修改任何内容都需要重新上传一次文件夹或者是压缩包zip】**

1.登录 Cloudflare  

找到计算AI-找到worker和pages
<img width="414" height="193" alt="image" src="https://github.com/user-attachments/assets/75c41546-cc6a-4a2f-9fa5-3632f0d89104" />
点击创建应用程序
<img width="1494" height="188" alt="image" src="https://github.com/user-attachments/assets/6ddd7c84-4a4f-4ddc-bd41-f2d550139999" />
点击下方的Get started 跳转到pages界面
<img width="1294" height="601" alt="image" src="https://github.com/user-attachments/assets/f5fdaa8d-d86a-471e-93de-9107db440443" />
选择第二个
<img width="1288" height="509" alt="image" src="https://github.com/user-attachments/assets/5f823410-7308-4425-9e77-a66646235e00" />

输入项目名称 

点击创建项目
<img width="1396" height="690" alt="image" src="https://github.com/user-attachments/assets/c10dc676-a06a-4a6b-bc62-f24239f454b0" />

**上传文件 【可上传zip包】 【可上传文件夹】**

<img width="1330" height="667" alt="image" src="https://github.com/user-attachments/assets/5dec9d85-9fcb-4b95-89c6-a7d8c57be661" />

**点击部署站点 完成**

**这样pages 上传部署方法就完成了**



----------------------------------------------------------------------

# cloudflare snip部署 【有snippets的必看】

点击自己的域名进入

<img width="1565" height="202" alt="image" src="https://github.com/user-attachments/assets/2483c2b7-3bb2-4cac-bdd6-38f8b31f4329" />

找到规则-snippets 点击创建片段

<img width="1652" height="716" alt="image" src="https://github.com/user-attachments/assets/9059a47d-77da-4ba4-82cc-03e8a8638c0f" />

输入片段名称【自己决定】

<img width="1920" height="878" alt="image" src="https://github.com/user-attachments/assets/f163e9ef-989b-4645-8ebc-eadf755f4b23" />

找到我项目的worker.js代码 打开它 复制代码 粘贴到snippets

选择片段规则-自定义规则

字段为主机名 运算符为等于 值为你的子域名+你的域名

例如：123为子域名 321.com为你的CF托管域名 

<img width="1920" height="914" alt="image" src="https://github.com/user-attachments/assets/1f858efe-a6ce-4bf6-8d62-0bfc462ef2b3" />

点击完成 保存更改

弹出修改 创建DNNS记录 

选择创建新代理DNS记录

类型为A 名称为你的子域名 ipv4 为192.0.2.1


<img width="640" height="459" alt="image" src="https://github.com/user-attachments/assets/f88ad346-30aa-41ef-9f7c-deb2453afbfe" />


**snippets部署结束**


------------------------------------------------------------------------

### 方法二：通过 GitHub Actions 部署（进阶）

*如果你熟悉 Wrangler CLI，可以直接 clone 本仓库并使用 `npx wrangler deploy`。*


------------------------------------------------------------------------------


# ⚖️ 免责声明

**本项目仅供技术交流与学习使用，请勿用于非法用途。使用本程序产生的任何后果由使用者自行承担。**


# 🙏 致谢

**基于 Cloudflare Workers 平台**

**感谢开源社区提供的优选 IP 思路**

**致谢Alexandre Kojève做的TCP流媒体优化**

**致谢天诚大佬COMLiang做的proxyip**

**感谢天诚交流群各位群友支持**
