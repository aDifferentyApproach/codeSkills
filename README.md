# python-good-code

编写或改写 Python 实现代码时使用的编码规则 skill：**担保一个正常需求得到一个好的代码实现。**

**好代码 = 设计精简 + 性能高效 + 实现简洁 + 对修改者友好（修改者含 AI 与人）**

## 这是什么

一份写给 AI 编码助手的规则集 + 知识层（Agent Skills / SKILL.md 开放格式）：

- **四维编码规则**：任务拆步与反贪心、复杂度与常数两层裁决、冗余消除、人机双重可维护
- **结构探针**：候选生成防漏选（状态压缩 / 模 k 计数 / 闭式直取 / 多次访问索引化 + 兜底问句）
- **patterns.md**：21 条算法思想目录（信号/形态索引表）
- **examples/**：正反对照式实现样例（❌ 反例代码块 + 问题诊断 vs ✅ 最小骨架）

## 效果（LeetCode 1–200 中 184 道 Python 题三口径对比测试）

| 指标 | 本 skill | 无 skill | 旧版规则 |
|---|---|---|---|
| 平均每题代码行 | **10.9** | 15.3（+40%） | 13.1（+20%） |
| 决策失误 | **0** | — | 多轴支配漏选、常数层误判等 |

方法：同一模型独立实现三份语料，程序化 diff + 全量本地 runner 验证（约 370 项断言）。

## 安装

复制整个目录到任意 skills 扫描目录即自动注册：

- Kimi Code：`~/.kimi-code/skills/python-good-code/`
- Claude Code：`~/.claude/skills/python-good-code/`
- 项目级：`<project>/.kimi-code/skills/` 或 `.agents/skills/`

## 结构

```
SKILL.md            规则本体：定位 / 何时不用 / 四维 / 探针
references/         知识层：思想目录、实现样例、两个升级模式（并行并发 / 架构分析，未实现）
assets/templates/   性能设计方案模板（方案筛选非平凡时强制留痕）
CHANGELOG.md        0.1.0 → 0.2.3 演化史
```

## 使用模式

默认基础模式（串行实现规则），编码时自动触发；两个升级模式由人显式开启后适用（规则位置见 references/）。

## License

MIT © 2026 aDifferentyApproach
