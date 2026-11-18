# KellyC Image Downloader — 个人 Fork 项目说明

- 正式源码仓：`keguzhi44-sketch/KellyC-Image-Downloader`
- 上游：`NC22/KellyC-Image-Downloader`
- 原始扩展版本：`1.2.9.5`（见 `extension/manifest.v3.all.json` 与 v2 清单）
- 许可证：`GPL-3.0`；保留原作者 LICENSE 与版权信息。
- 起始盘点基线：`master@7c6dc923cd79377c4808dfc685d1c8f5f7ed78ff`（2026-11-18，整理前）
- 当前阶段：**工程接管 / 结构与代码盘点**，不是产品功能发布。
- 实机状态：**尚未在用户 Chrome 实机验证**；不能认定 Fork 已可直接加载和使用。

## 目标
保留并理解通用页面图片提取、图片归类筛选、跨标签页记录、关联文档寻找原图、下载管理与网站专用解析规则。后续逐项决定保留/移除/修改哪些功能，不先行重写。

## 目录职责
```text
/
├── README.md / LICENSE              上游说明与授权（不改动）
├── extension/                       原版扩展源码、资源、MV2/MV3 清单
│   ├── manifest.v2.all.json
│   ├── manifest.v3.all.json
│   ├── lib/                         通用业务、存储、下载与站点解析
│   ├── widget/                      界面控件
│   ├── env/                         HTML/CSS/图片与初始化入口
│   └── _locales/                    英语、俄语
├── _build/                          原版 Windows MV3 后台合并脚本
├── AI_CONTEXT.md                    新 AI 会话入口（本 Fork）
├── COMPONENTS.md                    按职责映射模块（本 Fork）
├── PROJECT.md                       当前维护边界（本 Fork）
└── maintenance/                     代码盘点、待核实问题、验证与记录
```

## 构建与安装边界
上游 README 将 `extension/` 描述为可使用构建，但当前 Fork 不具备直接加载所需的完整 MV3 产物：缺少 `manifest.json`、`background.js`，两份清单还含缺失的 Joyreactor 引用。原始 `_build/merge.bg.v3.bat` 是 Windows 批处理。此处仅记录问题，尚未制作 Mac 构建替代程序或修复引用。

## 下一阶段准入
先解决当前构建入口与缺失文件的可解释性，再做真实 Chrome 加载测试。只有拿到可重复的测试结果，才能把原版版本标记为实机基线。原有代码仍是迁移前回退参照。

详见 `maintenance/CODE_INVENTORY.md`、`maintenance/ISSUES_AND_UNKNOWNS.md`、`maintenance/VALIDATION.md`。
