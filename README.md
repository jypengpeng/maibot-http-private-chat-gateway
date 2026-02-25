# 项目说明

本项目基于 [MaiBot](https://github.com/MaiM-with-u/MaiBot) 修改而来。

## 本仓库的主要改动

### 1) 新增外部 HTTP 私聊入口（非 QQ 入口）

- 新增接口：`POST /api/chat/external/private/message`
- 用途：允许第三方系统通过 HTTP 请求与机器人对话，不再依赖 QQ 侧消息入口。
- 支持内容：
  - 文本消息
  - 图片 URL（服务端下载后转为图片消息处理）

### 2) 复用原私聊逻辑与上下文

- 外部请求会被转换成和原系统兼容的私聊消息结构。
- 通过 `session_id` 映射稳定用户标识，同一 `session_id` 共享同一私聊上下文。
- 继续走原有私聊消息处理链路，保持行为一致。

### 3) 同步返回回复

- 接口以同步方式返回本次机器人回复内容。

### 4) 增加最简鉴权（适配公网）

- 接口支持以下鉴权头（二选一）：
  - `X-MaiBot-Token: <token>`
  - `Authorization: Bearer <token>`
- `token` 来源于配置中的 `maim_message.auth_token`。

## 兼容性说明

- 该仓库在 MaiBot 原有能力基础上扩展了 HTTP 聊天入口。
- 原有 QQ / WebUI 相关能力不作为本 README 的重点说明。
