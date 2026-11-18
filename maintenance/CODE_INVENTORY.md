# 源码与文件盘点 — 2026-11-18

## 范围、依据与置信度
只检查个人 Fork `master@7c6dc923cd79377c4808dfc685d1c8f5f7ed78ff` 的当前文件树、MV2/MV3 清单、上游文档和主要源码入口；**不是整仓逐行安全审计，也没有实机运行**。基于文件路径和源码首段推断的职责标为“初步”。

## 根目录
- `LICENSE`、`README.md`：GPLv3 及上游说明；README 表明原作者已将产品撤出扩展商店供个人继续使用。
- `extension/`：扩展运行所需脚本与素材。
- `_build/README.md`、`_build/merge.bg.v3.bat`：MV3 后台合并说明及 Windows 构建脚本。
- `.github/FUNDING.yml`：上游 GitHub 赞助配置（当前文件大小 0）；与运行无直接关系。
- 当前新增的 `AI_CONTEXT.md`、`PROJECT.md`、`COMPONENTS.md`、`maintenance/`：个人 Fork 维护层。

## 扩展清单和启动链
- `extension/manifest.v3.all.json`：MV3，版本 `1.2.9.5`，配置全站 content_scripts（`document_start`）、`downloads/storage/webRequest/declarativeNetRequest/tabs/unlimitedStorage`、`<all_urls>` 的 host_permissions、后台 `background.js`、popup `env/html/recorderPopup.html`、选项页 `env/html/recorderDownloader.html?tab=modules`。
- `extension/manifest.v2.all.json`：同版本 MV2，包含持久后台 scripts 与 `webRequestBlocking`。在现代 Chrome 不作为默认目标。
- `env/init/recorderFront.js`：页面初始化 `KellyPageWatchdog.exec()`；`env/init/recorderDownloader.js` 调用 `KellyDPage.init()`；`env/init/background.js` 调用 `KellyEDispetcher.init()`。
- MV3 构建流程设计：合并 `kellyTools.js`、`kellyDispetcher.js`、`kellyDispetcherNetRequest.js`、Joyreactor 专属后台模块、`kellyEDRecorder.js` 和 `env/init/background.js` 为 `extension/background.js`。这是构建意图，并非已验证的现行产物。

## 源码职责（实际存在的主要文件）
| 路径（相对 extension） | 规模（约） | 首轮观察 |
|---|---:|---|
| `lib/kellyFavItems.js` | 197 KB | 收藏库、分类/筛选、UI 和下载界面的组合控制器 |
| `lib/kellyGrabber.js` | 108 KB | 下载队列、状态、命名与取消 |
| `lib/kellyStorageManager.js` | 69 KB | 配置、收藏数据、导入导出、下载文件夹配置 |
| `lib/kellyTools.js` | 49 KB | 浏览器与网络操作辅助 |
| `lib/kellyDispetcher.js` | 41 KB | 后台消息及下载事件派发 |
| `lib/kellyDispetcherNetRequest.js` | 14 KB | MV3 网络规则、临时 Referer 相关处理 |
| `lib/kellyThreadWork.js` | 11 KB | 下载与关联文档任务调度 |
| `lib/kellyFastSave.js` | 15 KB | 快速保存 |
| `lib/kellyToolbar.js` / `kellyOptions.js` / `kellyAdditionsForm.js` | 9 / 22 / 7 KB | 工具栏、选项和附加表单 |
| `lib/recorder/kellyPageWatchdog.js` | 32 KB | 图片扫描、DOM 观察与解析适配器调用 |
| `lib/recorder/kellyLoadDocControll.js` | 25 KB | 从关联文档寻找原图 |
| `lib/recorder/kellyDPage.js` | 67 KB | 资源列表、分类过滤、操作与进度 |
| `lib/recorder/kellyEDRecorder.js` | 8 KB | 跨标签页收集器及 MV3 storage 缓存 |
| `lib/profiles/default.js` / `recorder.js` | 10 / 1 KB | 通用页面配置和记录器 profile |
| `widget/kellyImageView.js` / `kellyTileGrid.js` / `kellyTooltip.js` | 44 / 31 / 25 KB | 图片查看器、缩略图网格、提示控件 |

## 网站适配器
`extension/lib/recorder/filters/` 包含：
`9gag.js`、`artstation.js`、`bsky.js`、`deviantart.js`、`discord.js`、`ehentai.js`、`flickr.js`、`hfoundry.js`、`instagram.js`、`joyreactor.js`、`kemonoparty.js`、`pikabu.js`、`pixiv.js`、`reddit.js`、`twitter.js`、`vk.js`、`yandex.js` 以及 `_validators.js`、`README.md`。

- `pixiv.js`：按作品 ID 构造 `/ajax/illust/{id}/pages` 接口地址并尝试取得 `original` URL。
- `discord.js`：根据图片容器分别登记 preview、原始链接，并去除原图 URL 的某些尺寸参数。
- `twitter.js`：包含历史针对网页布局的 DOM 观察逻辑；**是否仍适配 X 的现行页面未验证**。
- `_validators.js`：共享 URL 分类规则、帮助链接和拦截的非图片 URL 标记。

## 资源与页面
- `extension/env/html/`：下载器、弹窗、选项、更新页及 `additions/`、`bookmarksParser/` 内的 HTML 片段。
- `extension/env/css/`：核心、单图/移动、浅色/深色、下载页、弹窗等样式。
- `extension/env/img/`：图标及一些上游图片素材；`extension/env/dynamic/dispetcher.js`：页面内消息与关闭确认处理。
- `extension/_locales/en/messages.json`、`ru/messages.json`：仅英语和俄语的现有界面本地化。
- `extension/lib/kellyNradiowaveBg.js`、`kellyCAbout.js`：存在，但在两份主要 manifest 的直接文件列表中未出现；是否被其它模块按需引用待核实。

## 数据与行为边界
- 此项目不是仅下载网页上现成的 img URL：它同时包含记录池、网页动态监听、按站点分类、额外请求关联文档、网络请求规则与收藏库。
- MV3 录制池使用 `chrome.storage.local` 类 API，存储项名可见 `kelly_cache_recorder`；不应因后台服务进程休眠而假定所有数据只在内存里。
- 当前项目明确请求宽泛网页权限；审查前不得给出“最小权限 / 只在点击时扫描”之类未实现保证。

详情与疑点见 `ISSUES_AND_UNKNOWNS.md`；所有信息均以实际源码优先。
