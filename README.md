<div style="font-size: 1.5rem;">
  中文 | <a href="./README.en.md">English</a>
</div>
</br>

**通知**：已发布 `1.0.0-beta` 版本，详见 [更新日志](https://github.com/AstraSurge/gpteams/releases)。我们将在近期更新 1.0.0 正式版本，涵盖 [开发看板](https://sharing.clickup.com/31625481/b/h/6-900200430791-2/756b82376fc8197) 所有 1.0.0 内容，并更新超详细的 wiki。

[在线演示网站](https://gpteams.astrasurge.com) (~~只有 [Astra Surge](https://astrasurge.com) 成员的组织邮箱才能登录~~ 1.0.0-beta.3 新增了聊天次数限制功能，现在每小时可以进行 3 次对话了, 域名已被 DNS 污染)

# GPTeams

![GPTeams Sign in Page](https://rorsch-1256426089.file.myqcloud.com/public/202303310632157.png)

![GPteams User Management Page](https://rorsch-1256426089.file.myqcloud.com/public/202303310634302.png)

![GPteams System Settings Page](https://rorsch-1256426089.file.myqcloud.com/public/202303310632530.png)

![GPTeams Chat Page](https://rorsch-1256426089.file.myqcloud.com/public/202303310632882.png)

GPTeams 是一个专为 ChatGPT 定制的基于 OpenAI API 的第三方客户端，旨在为用户提供 OPEN AI 官方 ChatGPT 网站未涵盖的团队协作功能。

## 特点

1. 提供完全免费的部署方案，利用 Firebase ~~和 Vercel 服务进行部署~~(经过实践，GPTeams无法支持Vercel的免费版，因为Vercel的免费版对 Serverless 函数的个数限制太低，而 GPTeams 计划日后添加更多好用的服务，Vercel的免费版不是长久之计，我们正在寻找另外一个可以轻松且免费部署 GPTeams 的平台)，免费额度足以满足小型团队需求（待实现，已排期）。
2. 支持通过 Google 账户登录、电话号码登录以及电子邮箱登录。
3. 设有管理员界面以便于管理用户，包括禁用/启用用户，删除用户等功能。
4. 系统设置页面，可以设置系统黑名单，白名单，OpenAI API Key，流量限制规则。
5. 用户可选择将本地某个会话同步至云端（待实现）。
6. 用户可将会话分享给团队中的其他成员（待实现）。

以上所述功能均已纳入开发计划，你可以在我们的 [开发看板](https://sharing.clickup.com/31625481/b/h/6-900200430791-2/756b82376fc8197) 上查看进度。如果你有更好的建议或意见，请随时通过 [contact@astrasurge.com](mailto:contact@astrasurge.com) 联系我们。

## 快速开始

### 环境变量

#### 编译期环境变量

- `VITE_APP_NAME`(可选设置)：应用名称，你可以将其更改为你想要的名称。修改后，名称会在各个地方（例如 HTML 标题、登录界面等）显示。

#### 运行时环境变量

以下变量是必需设置的，你可以在 [Firebase 官方文档](https://firebase.google.com/docs/web/setup?hl=zh-cn) 中获取 Firebase 项目配置信息：
```
FIREBASE_API_KEY
FIREBASE_AUTH_DOMAIN
FIREBASE_PROJECT_ID
FIREBASE_STORAGE_BUCKET
FIREBASE_MESSAGING_SENDER_ID
FIREBASE_APP_ID
FIREBASE_MEASUREMENT_ID
```
- `ROOT_ACCOUNT`(必需): 系统管理员账号，如果你通过 google 登录，那这里填 google 账号对应的邮箱。注意，如果你通过电话号码登录，这里需要填写你的**国家呼叫代码+电话号码**，如 `+8613498888888`。

- `GOOGLE_APPLICATION_CREDENTIALS_JSON`(必需): JSON 字符串格式的私钥文件, 必需。请查看 [Firebase 官方文档](https://firebase.google.com/docs/admin/setup?hl=zh-cn) 获取该信息。示例:
`
'{"type": "service_account", "project_id": "xxx", "private_key_id": "xxx", "private_key": "xxx", "client_email": "xxx", "client_id": "xxx", "auth_uri": "https://accounts.google.com/o/oauth2/auth", "token_uri": "https://oauth2.googleapis.com/token", "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs", "client_x509_cert_url": "xxx"}'`

- `PORT`(可选): 服务端口

其他变量请参阅 [chatgpt-web](https://github.com/Chanzhaoyu/chatgpt-web) 原项目的 README。

**注意**：最好不要使用其他变量，其他变量不受 GPTeams 保护，且可能在未来的版本删除。

### 使用 docker 部署

1. 将上文你想要设置的**编译期环境变量**填入 `.env` 中。
2. 构建 Docker 镜像：`sudo docker build -t gpteams .`
3. 将上文的运行时环境变量填写到 `env.list` 文件中用来注入运行时环境变量，启动：`sudo docker run --name gpteams -d -p 8000:3002 --env-file env.list gpteams`

## 鸣谢

[chatgpt-web 原项目](https://github.com/Chanzhaoyu/chatgpt-web)  
[Redon](https://github.com/Chanzhaoyu)

## License
MIT © [Astra Surge](./license)
