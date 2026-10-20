![pi-flash 封面](docs/images/pf-cover.png)

Pi Flash：极速的 Pi coding agent 桌面壳

> 本仓库是 [danielbill/pi-flash](https://github.com/danielbill/pi-flash) 的 fork。
> 上游只发 **Windows x64**；这里补了 **macOS（Apple Silicon）的 dmg 构建**，代码与许可证保持原样。

## 下载

| 平台 | 安装包 | 说明 |
|---|---|---|
| macOS（Apple Silicon） | [`pi-flash-<v>-darwin-arm64.dmg`](https://github.com/zcx960/pi-flash/releases/latest) | 本 fork 构建，拖进「应用程序」即用，**已内置 Node，无需另装** |
| macOS（Apple Silicon） | [`pi-flash-<v>-darwin-arm64.zip`](https://github.com/zcx960/pi-flash/releases/latest) | 绿色包，npm 薄壳 / 自动化脚本取用 |
| Windows x64 | [上游 Releases](https://github.com/danielbill/pi-flash/releases) | 由上游发布：`npm install -g pi-flash`（需 Node.js ≥ 22.19），或解压 zip 绿色包双击 `pi-flash.exe` |

每个包都附带 `.sha256` 校验和。

### macOS 首次打开（必读）

dmg 是 **ad-hoc 签名**（没有 Apple 开发者证书），首次启动会被 Gatekeeper 拦下，属预期行为：

1. 打开 dmg，把 `pi-flash` 拖进「应用程序」
2. **右键**点 pi-flash → **打开** → 弹窗里再点一次 **打开**

或者用一条命令免掉这一趟：

```bash
xattr -dr com.apple.quarantine /Applications/pi-flash.app
```

之后就能正常双击启动了。dmg 内也附了同样内容的说明文件。

## 演示

![pi-flash 演示动画](docs/images/pf-intro.gif)

## 自行构建 macOS 包

推 `v*` tag，或在 Actions 里手动跑 `release-macos`：

```bash
gh workflow run release-macos --ref main -f publish_release=true
```

- 不勾 `publish_release` 只产出 Actions artifact；勾上则按 `crates/app/Cargo.toml` 的版本建 / 更新 Release 并挂 dmg + zip
- 未配置 Apple 证书时走 **ad-hoc 签名**（用户首次打开需按上文放行）
- 配好 `APPLE_CERTIFICATE_P12`、`APPLE_CERTIFICATE_PASSWORD`、`APPLE_ID`、`APPLE_APP_SPECIFIC_PASSWORD`、`APPLE_TEAM_ID` 五个 secret 后自动转为 **Developer ID 签名 + 公证 + staple**，用户双击即可打开

自行从源码构建需要 Node.js ≥ 22.19 与 Rust stable（仅构建期依赖；产物包内已内置 Node 与 `vendor/pi` 运行时）。

发版细节见 [`docs/RELEASE.md`](docs/RELEASE.md)。

## 许可证

本项目以 **GPL-3.0-or-later** 许可证发布（见 [LICENSE](LICENSE)），继承自Zed项目。
你可以自由使用、修改、分发本软件，但任何基于本软件的衍生作品**必须**以GPL-3.0-or-later 开源。
不接受未经 Copyright Holder 同意的闭源分发。

第三方组件的版权与许可证声明见[THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md)。
