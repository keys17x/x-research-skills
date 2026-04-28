---
name: x-hangqing-guandian-sousuo
description: 在 X/Twitter 上搜索 BTC、ETH 或其他叙事的行情分析推文，筛掉明显噪音和营销内容，输出中文市场观点摘要、代表性推文、共识与分歧。
version: 1.0.0
author: Hermes Agent
license: MIT
platforms: [linux, macos]
prerequisites:
  commands: [uv]
  env_vars: []
metadata:
  hermes:
    tags: [twitter, x, crypto, market-analysis, research, chinese]
    homepage: https://github.com/public-clis/twitter-cli
---

# x行情观点搜索

用 `twitter-cli-browser` 这条路线，在 X/Twitter 上搜索 **BTC / ETH / 其他币种 / 某个叙事** 的行情分析推文，做基础筛选和中文提炼。

这个 skill 的目标不是“搜到推文”本身，而是：

- 搜到**值得看**的分析推文
- 过滤明显噪音、广告、口号式喊单
- 提炼出**主流观点、分歧点、关键价位/逻辑**
- 输出一版适合快速阅读的**中文研究摘要**

## 适用场景

适合：
- 快速看 BTC / ETH 当天市场讨论焦点
- 搜某个币或叙事最近的分析观点
- 为内容创作、选题、评论互动做信息准备
- 给进一步的账号筛选或内容转写提供样本

不适合：
- 直接拿结果当交易指令
- 把所有推文观点当事实
- 在样本极小的冷门币上强行下结论

## 推荐输入格式

最实用的输入一般包含这几个字段：

- 标的：`BTC` / `ETH` / `SOL` / `ETH/BTC` / 某叙事
- 时间范围：最近 `24h` / `3d` / `7d`
- 样本量：`10` / `20` / `50`
- 风格偏好：技术分析 / 宏观 / 链上 / 混合
- 语言：英文优先 / 中英混合

如果用户说得很简单，比如：
- “搜一下 BTC 的行情分析推文”
- “看看 ETH 最近大家怎么分析”

默认做法：
- 时间范围按最近 `24h-7d` 的可得结果处理
- 样本量先抓 `10-20`
- 以英文分析推文为主
- 输出中文摘要

## 搜索策略

不要只搜一个词。围绕目标自动扩展搜索词，常用模板：

### BTC 示例

```bash
twitter search "BTC analysis" --max 10 --yaml
twitter search "BTC outlook" --max 10 --yaml
twitter search "BTC chart" --max 10 --yaml
twitter search "BTC setup" --max 10 --yaml
twitter search "BTC bearish" --max 10 --yaml
twitter search "BTC bullish" --max 10 --yaml
```

### ETH 示例

```bash
twitter search "ETH analysis" --max 10 --yaml
twitter search "ETH outlook" --max 10 --yaml
twitter search "ETH chart" --max 10 --yaml
twitter search "ETH/BTC" --max 10 --yaml
```

### 叙事 / 主题示例

```bash
twitter search "AI agent tokens" --max 10 --yaml
twitter search "altseason analysis" --max 10 --yaml
twitter search "macro crypto outlook" --max 10 --yaml
```

## 执行流程

### Step 1: 确认认证可用

先检查 `twitter-cli-browser` 这条链路是否可用：

```bash
twitter status
twitter whoami
```

实战里更稳的默认做法是**直接显式指定浏览器**，尤其在搜索命令上：

```bash
TWITTER_BROWSER=chrome twitter status
TWITTER_BROWSER=chrome twitter search "BTC analysis" --max 10 --yaml
```

如果失败：
- 优先尝试 `TWITTER_BROWSER=chrome twitter status`
- 其次检查浏览器是否登录 x.com
- macOS 上留意 Keychain 权限
- 如果 `status` 偶发超时，但 `search` 能跑通，不要立刻判死；先直接用小样本搜索验证一次

### Step 2: 生成多组搜索词

围绕目标生成 `analysis / chart / outlook / setup / bullish / bearish` 等组合。

原则：
- 不要只搜一个词
- 对 BTC/ETH 这类主流币，至少跑 2-4 组搜索
- 如果结果太杂，优先保留 `analysis`、`chart`、`outlook`

### Step 3: 抓取结构化结果

优先用：

```bash
twitter search "BTC analysis" --max 10 --yaml
```

建议：
- 搜索时控制样本量，先小后大
- 一般先从 `--max 5` 或 `--max 10` 开始
- 需要节省 token 时，用 `twitter -c ...`
- 如果连续并发多组搜索容易超时，改成串行或只保留 `analysis / chart / outlook` 这 2-3 组高价值关键词
- 优先保留最近 24h 内、带图表、带关键价位/结构描述的内容

### Step 4: 基础筛选

优先保留：
- 有明确分析观点的推文
- 提到关键价位 / 趋势 / 背离 / 支撑阻力 / 结构判断的内容
- 带图表或带逻辑展开的内容

优先剔除：
- 纯广告 / 引流 / 带群 / 卖课
- 只有情绪口号，没有分析过程
- 明显和目标无关
- 高度重复的同类表述
- 单纯新闻转发、没有作者自身判断

### Step 5: 做观点聚类

把保留下来的内容分成这些常见桶：
- 偏多
- 偏空
- 震荡等待确认
- 相对强弱（如 ETH/BTC）
- 宏观 / 周期判断
- 纯噪音 / 营销

### Step 6: 提炼市场信息骨架

不要围着推文本身复述，要围着“问题结构”总结。典型骨架：
- 当前主流是偏多、偏空还是分歧
- 大家最常提到哪些关键价位 / 指标 / 结构
- 市场当前最大的争议点是什么
- 哪些推文提供了真正的信息增量

### Step 7: 输出中文结果

最终输出要紧凑、清楚、可继续使用。默认包含：

1. 一句话结论
2. 主流观点（2-4 条）
3. 值得看的代表性推文（作者 + 核心观点）
4. 共识与分歧
5. 风险提醒

## 推荐输出模板

```markdown
### BTC 行情观点搜索结果
**时间范围**：最近24h
**样本量**：抓取 24 条，筛后保留 8 条

**一句话结论**：
当前市场整体偏谨慎，短线略偏空，核心分歧在于关键支撑位能否守住。

**主流观点**
1. BTC 出现背离风险
2. 周末反弹可信度不足
3. 若守住关键位，仍有短线反抽空间

**值得看的推文**
- `@xxx`：认为 BTC 正在形成 bear flag，跌破关键支撑风险加大
- `@yyy`：认为短周期均线修复，仍可看技术性反弹
- `@zzz`：从更大级别结构看，趋势还没彻底转坏

**共识与分歧**
- 共识：某个支撑/阻力位很关键
- 分歧：当前是洗盘还是转弱确认

**风险提醒**
- 样本里有营销/引流内容，不能直接把 X 情绪当结论
- 很多观点基于短周期图表，噪音较大
```

## 质量标准

产出时尽量满足这些标准：
- 先说结论，再补细节
- 少空话，多信息密度
- 明确区分“市场在说什么”和“事实已经发生了什么”
- 不替用户喊单
- 不把营销号的情绪表达包装成严肃结论

## 默认工作方式

如果用户没有特别说明，默认：
- 搜 2-4 组关键词
- 每组抓 5-10 条
- 做基础筛选
- 输出中文摘要
- 如发现高质量作者反复出现，建议用户进一步跑 `x高质量分析账号筛选`
- 如用户想把结果变成内容，建议转入 `x推文研究转内容`

## 风险与边界

- 这是**非官方 X 访问路线**，稳定性不如官方 API
- 结果高度依赖当前时间点、平台推荐和搜索可见性
- 推文观点中会混入营销号、机器人号、广告号
- 这个 skill 用于研究参考，不用于直接给买卖指令

## 与其他 skill 的关系

- 上游依赖：`twitter-cli-browser`
- 下游可衔接：
  - `x高质量分析账号筛选`
  - `x推文研究转内容`

一句话：
**先用这个 skill 找“这次大家在说什么”，再决定要不要继续筛账号或转内容。**
