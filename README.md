# OmniRoute for LazyCat

本仓库将 [OmniRoute](https://github.com/diegosouzapw/OmniRoute) 打包为 LazyCat LPK v2，并自动发布到喵喵商店。

## 当前版本

- 包名：`community.lazycat.app.omniroute`
- OmniRoute：`3.8.49`
- 主镜像：`docker.1ms.run/diegosouzapw/omniroute:3.8.49`
- 目标架构：Linux amd64

OmniRoute 提供统一的 AI Provider 路由、控制台、OpenAI 兼容 API、MCP 与 A2A 能力。应用数据保存在 `/lzcapp/var/data`，内部 Redis 数据保存在 `/lzcapp/var/redis`。

## 安装设置

安装向导提供以下参数：

- 初始管理员密码
- Node.js 堆内存上限
- 是否为 `/v1` 接口强制启用 API Key
- 是否允许访问私有网络中的自托管 Provider
- 可选自定义公开域名；留空时使用懒猫应用域名
- 时区，默认 `Asia/Shanghai`

内部 JWT、API Key 加密、数据库加密和 WebSocket bridge 密钥由 LazyCat 的 `stable_secret` 自动生成。按项目要求，本包不注入免密登录，也不注入 LazyCat 文件选择器拦截脚本。

## 自动发布

GitHub Actions 每日检查 `docker.io/diegosouzapw/omniroute` 的稳定 SemVer 标签。发现新版本后会更新 Manifest、构建版本化 GitHub Release LPK，并仅同步到喵喵商店。Redis 使用固定的 LazyCat Registry 镜像，不参与自动更新。

工作流需要以下 GitHub Secrets：

- `APPSTORE_URL`
- `APPSTORE_TOKEN`
- `APP_ID`（可选）
- `PRIVATE_STORE_GROUP_CODES`（可选）

## 本地构建

```bash
lzc-cli project release -o .lazycat-build/omniroute.lpk
lzc-cli lpk info .lazycat-build/omniroute.lpk
```

## License

OmniRoute 及本仓库均采用 MIT License。
