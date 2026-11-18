# 检查与验证记录

## 2026-11-18：接管盘点

- 读取范围：个人 Fork 当前 master 及相关上游 README、两份 manifest 模板、`_build`、`lib`、`recorder`、`filters`、`widget`、`env` 的文件清单和关键源码入口。
- 已完成：核对 GitHub Fork 与上游归属；确认许可证；确认两份清单版本 `1.2.9.5`；核对关键目录、站点适配器、build 脚本；列出清单缺失引用和构建产物缺失；生成个人维护说明。
- 不变：上游 `README.md`、`LICENSE`、`extension/`、`_build/` 所有原始文件均未改动、移动或删除。
- 验证结果：**静态盘点通过，Chrome 可运行性未验证。**
- 不能声明：已经构建成功、Chrome 可以直接加载、实际网站抓取正常、可安全移除可选代码。
- 恢复基线：整理前 Fork `master@7c6dc923cd79377c4808dfc685d1c8f5f7ed78ff`。如以后发现文档不准确，优先纠正文档，不覆盖上游源码。
- 失败知识检查：本轮没有实际运行失败路线，不新增中央 Pitfall / Evidence。缺失构建文件为 **接管时观察到的结构事实**，记录于 `ISSUES_AND_UNKNOWNS.md`，不是复现过的程序故障。
