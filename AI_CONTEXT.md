# AI_CONTEXT — KellyC Image Downloader (personal fork)

本仓库是 `NC22/KellyC-Image-Downloader` 的个人 Fork。目标是以原有图片发现与批量下载能力为基础，逐步维护可长期使用的个人 Chrome 扩展。

## 事实优先级
1. 当前分支实际源码及浏览器清单；
2. 本仓 `PROJECT.md` 与 `maintenance/`；
3. `keguzhi44-sketch/tooling-handbook` 当前规范；
4. 原作者 README、Wiki 与历史说明（仅作为上游资料）。

每项新的正式工程任务先重新读取 `tooling-handbook/CATALOG.md`、`ROUTING.md`、`GLOBAL_RULES.md`、`CONSTRUCTION_STANDARD.md`、`FAILURE_EVIDENCE_STANDARD.md`、`PRACTICE_LIBRARY.md` 与相关 `practices/*.md`。不得用本文件代替重新读取规范。

## 进入本仓的最小阅读路径
- `PROJECT.md` → `COMPONENTS.md` → `maintenance/manifest.json`；
- 评估现状：`maintenance/CODE_INVENTORY.md`、`maintenance/ISSUES_AND_UNKNOWNS.md`、`maintenance/VALIDATION.md`；
- 再按任务进入 `extension/manifest.v3.all.json`、`extension/manifest.v2.all.json` 及对应源码。
- 上游 `README.md`、`extension/README.md` 和 `_build/README.md` 保留，区别于本 Fork 的维护文档。

## 边界
- **截至 2026-11-18 的首轮整理只新增维护文档，没有修改或移动任何原作者运行源码。**
- `extension/` 是上游实际源码与资源目录；`_build/` 是上游构建脚本，不是可直接加载扩展的根目录。
- 不要把根目录或 `maintenance/manifest.json` 当作 Chrome 清单。原仓当前尚无可直接加载的 `extension/manifest.json` 和生成好的 `extension/background.js`。
- 不因文件名古怪、俄语注释、TODO 或暂未理解而删除、改名或移动。
- 若以后拟迁移目录，先列出完整引用关系，生成可安装产物并在 Chrome 验证后再动源码。
- 不擅自清除作者声明、GPL-3.0 许可证或第三方授权文件。
- 对未验证的功能、风险、死代码和根因须明确写“待核实”，不要直接当作已证实缺陷。
- 普通调试日志、账号数据、下载记录、cookies、state、token 不进 Git；Evidence 按中央规范处理。

## 项目归属
- 源码唯一权威：`keguzhi44-sketch/KellyC-Image-Downloader`；
- 个人工具索引：`keguzhi44-sketch/mac-utilities/browser-tools/kellyc-image-downloader/`（只保存导向，无源码副本）；
- 总索引：`keguzhi44-sketch/tooling-handbook/CATALOG.md`。
