# openclaw-onebot

将 **OneBot v11 协议**（QQ/Lagrange.Core、go-cqhttp 等）接入 [OpenClaw](https://openclaw.ai) Gateway 的渠道插件。

[![npm version](https://img.shields.io/npm/v/openclaw-onebot.svg)](https://www.npmjs.com/package/openclaw-onebot)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## 功能

- ✅ 私聊：所有消息 AI 都会回复
- ✅ 群聊：仅当用户 @ 机器人时回复（可配置）
- ✅ 正向 / 反向 WebSocket 连接
- ✅ TUI 配置向导：`openclaw onebot setup`
- ✅ 新成员入群欢迎
- ✅ Agent 工具：`onebot_send_text`、`onebot_send_image`、`onebot_upload_file`

## 安装

```bash
openclaw plugins install openclaw-onebot
```

或从 GitHub 安装：

```bash
openclaw plugins install https://github.com/LSTM-Kirigaya/openclaw-onebot.git
```

## 配置

### 方式一：TUI 向导（推荐）

```bash
openclaw onebot setup
```

交互式输入：连接类型、主机、端口、Access Token。

### 方式二：手动编辑 `~/.openclaw/openclaw.json`

```json
{
  "channels": {
    "onebot": {
      "type": "forward-websocket",
      "host": "127.0.0.1",
      "port": 3001,
      "accessToken": "可选",
      "enabled": true,
      "requireMention": true,
      "groupIncrease": {
        "enabled": true,
        "message": "欢迎 {userId} 加入群聊！"
      }
    }
  }
}
```

### 连接类型

| 类型 | 说明 |
|------|------|
| `forward-websocket` | 插件主动连接 OneBot（go-cqhttp、Lagrange.Core 正向 WS） |
| `backward-websocket` | 插件作为服务端，OneBot 连接过来 |

### 环境变量

可替代配置文件，适用于 Lagrange 等：

| 变量 | 说明 |
|------|------|
| `LAGRANGE_WS_TYPE` | forward-websocket / backward-websocket |
| `LAGRANGE_WS_HOST` | 主机地址 |
| `LAGRANGE_WS_PORT` | 端口 |
| `LAGRANGE_WS_ACCESS_TOKEN` | 访问令牌 |

## 使用

1. 安装并配置
2. 重启 Gateway：`openclaw gateway restart`
3. 在 QQ 私聊或群聊中发消息（群聊需 @ 机器人）

## Agent 工具

| 工具 | 说明 |
|------|------|
| `onebot_send_text` | 发送文本，target: `user:QQ号` 或 `group:群号` |
| `onebot_send_image` | 发送图片，image: 路径/URL/base64 |
| `onebot_upload_file` | 上传文件，file: 本地路径，name: 文件名 |

## 测试连接

项目内提供测试脚本（需 `.env` 或环境变量）：

```bash
cd openclaw-onebot
npm run test:connect
```

## 协议参考

- [OneBot 11](https://github.com/botuniverse/onebot-11)
- [go-cqhttp](https://docs.go-cqhttp.org/)
- [Lagrange.Core](https://github.com/LSTM-Kirigaya/Lagrange.Core)

## License

MIT © [LSTM-Kirigaya](https://github.com/LSTM-Kirigaya)
