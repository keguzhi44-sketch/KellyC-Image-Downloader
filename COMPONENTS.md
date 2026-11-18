# 组件导览（首轮静态盘点）

| 组件 | 关键位置 | 已观察到的职责 | 后续处理 |
|---|---|---|---|
| 页面图片扫描 | `extension/lib/recorder/kellyPageWatchdog.js` | 图片/部分视频 URL 发现、DOM 监听、图片类型归类、调用站点适配器 | 核心，保留 |
| 页面记录与跨标签页池 | `extension/lib/recorder/kellyEDRecorder.js` | 收集图片记录，MV3 使用 storage.local 缓存 | 核心，先验证 |
| 关联文档原图发现 | `extension/lib/recorder/kellyLoadDocControll.js` | 加载缩略图关联文档，查找或确认可能的原图 | 重要，先验证 |
| 下载展示页控制 | `extension/lib/recorder/kellyDPage.js` | 提取结果分类、过滤、链接处理、页面进度 | 核心，保留 |
| 批量下载队列 | `extension/lib/kellyGrabber.js` | 下载项、状态、文件命名、失败与取消 | 核心，保留 |
| 后台 API 派发 | `extension/lib/kellyDispetcher.js` | 消息、下载事件、网络相关任务 | 核心，需验证 MV3 |
| MV3 网络规则 | `extension/lib/kellyDispetcherNetRequest.js` | declarativeNetRequest 会话规则、Referer 处理 | 复杂，重点审查 |
| 配置与收藏库 | `extension/lib/kellyStorageManager.js` | 本地数据、配置、分类、导入导出 | 需要划清保留范围 |
| 收藏/主界面框架 | `extension/lib/kellyFavItems.js` | 大型组合 UI/数据控制器 | 暂不拆分 |
| 快速保存 | `extension/lib/kellyFastSave.js` | 单图快速保存相关操作 | 后续验证 |
| 网页工具与 API 包装 | `extension/lib/kellyTools.js` | 浏览器 API、请求、通用辅助函数 | 核心共用 |
| 任务线程 | `extension/lib/kellyThreadWork.js` | 批量请求的任务安排和进度 | 先验证 |
| 界面控件 | `extension/widget/*.js`、`extension/lib/kellyToolbar.js`、`kellyOptions.js`、`kellyAdditionsForm.js` | 图片预览、网格、提示、工具栏与选项 | 保留 |
| 浏览器入口与页面 | `extension/env/init/`、`extension/env/html/`、`extension/env/css/` | popup、下载管理、页面注入、样式 | 保留原路径 |
| 网站解析 | `extension/lib/recorder/filters/*.js` | Pixiv、Discord 等网站的图片类型与原图识别 | 独立逐站维护 |
| Profiles | `extension/lib/profiles/default.js`、`recorder.js` | 通用配置和记录器环境 | 保留 |
| 构建 | `_build/merge.bg.v3.bat`、两份 manifest 模板 | 组装 MV3 后台、选择清单 | 暂不更动 |

**注意：** 上表是模块职责索引，不是运行验证结论。实际调用链和可删减范围必须先看源码、清单与对应验证报告。
