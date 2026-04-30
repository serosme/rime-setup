# RIME Setup — AGENTS.md

## 仓库用途

个人 RIME（中州韻）输入法配置补丁，基于 [rime-ice](https://github.com/iDvel/rime-ice)。每个 `.custom.yaml` 文件是一个 RIME 补丁，在运行时覆盖/追加上游默认值 — 本地无需构建步骤。

## 关键文件

| 文件                              | 用途                                                      |
| --------------------------------- | --------------------------------------------------------- |
| `default.custom.yaml`             | 方案列表、每页候选数 (7)、快捷键                          |
| `double_pinyin_flypy.custom.yaml` | 开关切换（中/英、¥/$、简/繁、表情、半角/全角、正常/单字） |
| `weasel.custom.yaml`              | Weasel（Windows 前端）：应用英文模式、配色方案、标签格式  |

## CI / 发布

- **工作流**: `.github/workflows/release-please.yml`
  - 推送到 `main` 触发 `release-please-action`（simple release 类型）
  - 创建 Release 后，`build` job 运行：合并上游 rime-ice + 本地补丁，打包为 `rime-config-<tag>.zip`，上传到 Release
- **Release 产物**: `rime-config-v*.zip` 附加到每个 GitHub Release

## 提交规范

必须遵循 Conventional Commits，因为 `release-please` 根据提交信息自动决定版本号：

- `feat:` → minor 版本 bump
- `fix:` → patch 版本 bump
- `feat!:` 或 `fix!:` → major 版本 bump
- `ci:` / `docs:` / `style:` / `refactor:` / `chore:` → 不触发 release
