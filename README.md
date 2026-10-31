# qq-bridge-official

> **这是 [qq-bridge](https://github.com/juju114514/qq-bridge) 的「官方通道」分仓库。**
> 主仓库对官方通道**上锁中**（见 [主仓库 LOCK.md](https://github.com/juju114514/qq-bridge/blob/main/LOCK.md)），
> 后续开发与真机验证都在这里做，**做完一次性合并回主仓库并解锁**。

## 一、这个通道是什么

QQ **官方机器人**通道（QQ Bot API v2）—— 与"个人号"（SnowLuma / OneBot）并列的第二条入口。

| | 个人号 | 官方机器人（本仓库） |
| --- | --- | --- |
| 协议 | OneBot / SnowLuma | QQ Bot API v2（官方） |
| 身份 | 你的 QQ 号 | 官方机器人（AppID + AppSecret） |
| 群范围 | 你在的群 | 机器人被拉进的群 / 频道 |
| 封号风险 | 有 | 官方许可，风险低得多 |
| 本仓库状态 | — | 🔧 **调试与维修中** |

## 二、当前状态

| 项 | 状态 |
| --- | --- |
| 代码 | ✅ 审计的 3 个缺口已修（owner openid / 按通道身份 / message_id 去重） |
| 真机 e2e | ⏳ **正在做** |
| 预计 | **2026-11-03 前** |
| 主仓库口径 | 🔒 上锁，不宣传、不承诺 |

**在 e2e 通过前，请按「未验证」对待。**

## 三、这个仓库里有什么

```
src/qqbot-official.js        事件解析（GROUP_AT_MESSAGE_CREATE / C2C_MESSAGE_CREATE）
src/official-transport.js    WebSocket 传输、被动回复 seq、媒体发送
src/official-media.js        图片/文件
src/official-proactive.js    定时播报 + 撤回
docs/audits/                 审计报告（缺口、根因、修法）
docs/validation/             e2e 验证清单与记录
```

> ⚠️ 这些文件是从主仓库**提取的副本**，不是独立可运行的项目：
> 它们依赖主仓库的 `config.js` / `safe-fetch.js` / `bridge.js` 上下文。
> 本仓库的用途是**开发与验证**，最终以主仓库为准。

## 四、合并回主仓库的条件（解锁）

1. `docs/validation/official-e2e.md` 里四条全过（@ / 私聊 / 发图 / 白名单拒绝）
2. 身份正确：`[official] 自我身份已设置`，prompt 里是官方机器人身份
3. owner 生效：`official.ownerOpenid` 配置后管理员指令有效
4. 去重生效：断线重连不重复回复

四条全绿后：一次性把差异合并回主仓库 → 改主仓库 LOCK.md 状态 → 发版解锁 → 归档本仓库。

## 五、免责声明

本项目同样按 MIT **「现状（AS IS）」**提供，无任何担保。
即使在本仓库里验证通过的功能，也**不构成对任何具体使用场景的承诺**；
平台风险（账号限制等）与使用后果由使用者自行承担。详见主仓库 LOCK.md 的免责声明一节。

## 六、相关链接

- 主仓库：<https://github.com/juju114514/qq-bridge>
- 主仓库锁：<https://github.com/juju114514/qq-bridge/blob/main/LOCK.md>
- 审计报告：[docs/audits/official-channel-audit-2026-10-31.md](docs/audits/official-channel-audit-2026-10-31.md)