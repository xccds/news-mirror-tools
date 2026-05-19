# news-mirror-tools

在终端中自动抓取《新闻联播》全文，并对新闻进行结构化理性分析，识别宣传技巧与逻辑漏洞，帮助建立独立思考能力。

适用于 **OpenCode** / **Claude Code** 等 AI 编码助手。

## 文件结构

```
news-mirror-tools/
  README.md
  skills/                  ← 数据抓取流程定义
    xinwen-lianbo-transcript/  抓取新闻联播文字稿
    people-daily-history/      抓取人民日报历史
  commands/                ← 封装好的分析任务指令
    getnews.md                 抓取 + 保存 + 编号摘要
    analysis.md                6层逻辑解构分析
    newsjok.md                 黑色幽默解构
```

- **Skill** = 告诉 agent 数据从哪里拿、怎么拿
- **Command** = 一句指令触发完整分析任务，内部自动调用 Skill 完成数据采集

## 核心工作流

三条命令构成一条完整的分析链路：

```
/getnews 昨天
  → 自动调用 xinwen-lianbo-transcript 技能
  → 抓取指定日期新闻联播全文
  → 保存到本地 md 文件
  → 在终端输出带编号的摘要

/analysis 1
  → 读取上一步生成的 md 文件
  → 对第1条新闻进行6层解构（事实、逻辑、语言、意图、推断、讽刺）
  → 调用搜索工具验证可核查事实
  → 在终端输出完整分析

/newsjok 1
  → 读取同一份 md 文件
  → 对第1条新闻进行荒诞文学风格的幽默解构
  → 在终端输出段子
```

## 如何使用

### 安装

将 skills 和 commands 复制到你的项目 `.opencode/` 目录下：

```bash
cp -r skills/*   你的项目/.opencode/skill/
cp -r commands/* 你的项目/.opencode/commands/
```

### 日常使用

在终端中对 agent 说：

```
/getnews 昨天
/analysis 1
/newsjok 1
```

命令参数说明：
- `/getnews <时间>` — 时间支持 "昨天"、"前天"、"20260517" 等格式
- `/analysis <编号>` — 编号对应 getnews 输出的摘要序号
- `/newsjok <编号>` — 同上

## 免责声明

本工具仅用于个人学习和研究。所有抓取内容的版权归央视网/人民网所有。

## 依赖

- OpenCode 或兼容的 AI 编码助手
- 网络连接
