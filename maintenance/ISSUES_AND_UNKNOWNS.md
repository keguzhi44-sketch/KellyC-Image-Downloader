# 疑点、遗留项与后续核实清单 — 2026-11-18

本表**不是已确认 Bug 列表**。区分可直接确认的源码结构事实与必须实机再判断的风险；不据此擅自删除代码。

## A. 已确认的结构事实（优先级高）
1. `extension/` 中没有 `manifest.json`，只有 `manifest.v2.all.json` 和 `manifest.v3.all.json`；因此不能直接对 `extension/` 点击“加载已解压的扩展程序”。
2. MV3 清单指定 `background.js`，但 `extension/background.js` 不在当前仓库中；`_build/merge.bg.v3.bat` 说明应由多个源码文件合并生成，脚本仅提供 Windows .bat 形式，未提供原生 Mac 构建入口。
3. 两份 manifest 的 content_scripts 均引用不存在的 `lib/profiles/joyreactor.js`、`lib/profiles/joyreactor.unlock.js`、`lib/profiles/topjoyreactor.js`、`env/init/joyreactorFront.js`；MV2 后台及 MV3 合并脚本额外引用缺失的 `lib/profiles/joyreactor.unlock.d.js`。这里需要决定保留上游依赖、取得授权源码，还是有依据地移除可选 profile。
4. 原版 `_build/README.md` 将上述 Joyreactor 脚本描述为 optional，但目前**没有做移除后的运行验证**；“optional”不等于可以直接删掉所有相关逻辑。
5. `lib/recorder/filters/_validators.js` 中在 `fanbox.cc` 规则之后存在孤立的 `https://thumbs.hentai-foundry.com/thumb.php?... ` 文字，疑似调试遗留。需核对 JS 实际解析效果和规则加载结果，不用猜测替代。
6. `env/dynamic/dispetcher.js` 使用 `window.postMessage` 和页面内注入/变量读取入口；仅凭用途不能断言安全或危险，后续按消息来源与跨域信任边界审查。
7. `lib/kellyNradiowaveBg.js` 的示例背景图片名在所列 `env/img/` 中未出现，且不在主要 manifest 直接加载列表；是否为历史未使用的附属模块待核实。

## B. 高价值的待验证设计边界
- `document_start` 且匹配全部 HTTP(S) 网站，清单注入的 JS 数量多；资源开销及与网页的冲突需在真实页面衡量。
- `KellyEDispetcherNetRequest.js` 使用 MV3 declarativeNetRequest 会话规则，并有关于跳转、Referer、keep-alive 的 TODO；先验证下载链条，不贸然改变网络规则。
- `kellyPageWatchdog.js` 设有视频地址识别，但 `kellyDPage.js` 把 `srcVideo` 默认标为排除类；不能直接将此工具说成完整视频下载器。
- `kellyFavItems.js` 既有收藏/分类，又参与界面构建；`kellyStorageManager.js` 管理多种存储格式。贸然删除“收藏”可能破坏下载 UI 或配置。
- `recorderPopup.js` 多标签页录制分支中存在固定 1000ms 超时与作者 TODO；是否造成真实抓取缺失，必须测试。
- 某些站点脚本（如 Twitter）有历史页面 DOM 选择器，不能因文件存在就宣称适配当前版本。
- 宽泛 host_permissions、downloads、webRequest、declarativeNetRequest、storage 等能力需要按实际使用界定；不是隐私审计结论。
- 多处俄语注释、旧作者链接、更新页、旧商店地址属于遗留内容；只在明确不影响运行后再整理。

## C. 尚未完成的验证
- 没有生成 MV3 最小可加载构建，没有 Chrome 实机打开弹窗。
- 没有执行 JavaScript 全量语法测试、依赖引用完整性测试、跨站实际抓图/防盗链/下载压力测试。
- 没有检查所有路径是否真正动态引用或每个适配器是否仍可运行；此次是第一轮结构与关键入口代码盘点。
- 没有完成隐私与安全全量源码审计；不能用“未见可疑代码”替代安全结论。

## D. 暂定优先顺序（未来单独立项）
1. 单独制作可重复的 MV3 构建入口和完整文件引用报告，不改图片业务逻辑；
2. Chrome 最小加载验证（popup → 当前页识图 → 下载）；
3. 原图/关联文档链条与跨标签记录验证；
4. 站点适配器逐个验证；
5. 根据已证实无用、重复、失败的组件再提出精简/拆分方案。

本轮**不执行**上述项目。
