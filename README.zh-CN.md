<p align="center">
  <img src="assets/hero.png" alt="反防御写作：书页长成树，根系连接证据。充分展开思想，保留事实依据。" width="100%">
</p>

<h1 align="center">反防御写作 · Anti-Defensive Writing</h1>

<p align="center"><strong>把有价值的思想写充分，让解释、证据和作者声音共同成立。</strong></p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-23453B" alt="MIT 许可"></a>
  <a href="skill/anti-defensive-writing/SKILL.md"><img src="https://img.shields.io/badge/format-SKILL.md-16324F" alt="SKILL.md 格式"></a>
  <a href="README.md"><img src="https://img.shields.io/badge/docs-English%20%2F%20中文-A4472D" alt="中英文文档"></a>
</p>

<p align="center"><a href="README.md">English</a> · <strong>简体中文</strong></p>
<p align="center"><a href="#quick-start">快速开始</a> · <a href="#examples">改写对照</a> · <a href="#method">方法说明</a> · <a href="#usage">调用示例</a> · <a href="#provenance">项目来源</a></p>

这是一个可独立安装的 AI 写作 Skill。它帮助作者发展值得推进的想法，把关系讲清楚，并根据证据决定表达力度；处理构思时提前退让、正文反复设限、无依据地收窄题目，以及审改后文字更顺却内容更薄的问题。

它始终追问：**这一段应该让读者理解什么、经历什么，正文有没有真正写出来？**

本仓库是 **git-zyyang 基于 [Kiterlin/anti-defensive-writing](https://github.com/Kiterlin/anti-defensive-writing) 的适配版本**。保留上游对主张、限定与证据强度的处理，进一步纳入构思推进、实质审改、理论深度和作者声音保护。[查看来源说明](skill/anti-defensive-writing/references/upstream.md)。

## 目录

- [为什么需要反防御写作](#why)
- [快速开始](#quick-start)
- [改写对照](#examples)
- [具体怎么判断](#method)
- [适用场景](#scenarios)
- [直接可用的调用示例](#usage)
- [接入日常写作流程](#integration)
- [安装、更新与移除](#installation)
- [文件结构与验证](#files)
- [常见问题](#faq)
- [项目来源](#provenance)
- [贡献与许可](#contributing)

<a id="why"></a>

## 为什么需要反防御写作

AI 辅助写作有时会把注意力放在预防质疑上。刚提出一个判断，就接上一串“不能说明”“不意味着”“仍需谨慎”；发现相似文献，还没有比较研究问题和解释，就建议缩小范围；精修时删掉重复表达，也一并删掉了原本支撑论证的文献、历史和具体过程。

这些问题牵涉作者如何思考和表达。反防御写作要求助手发展有依据的论证，判断每个限定的具体作用，并检查修改损失了什么。

| 遇到的情况 | Skill 引导助手做什么 |
|---|---|
| 因为已有相近题目，就否定一个值得推进的想法 | 比较实际问题、解释、方法与贡献，再判断可推进之处。 |
| 观点后面不断补上空泛提醒、自我贬低 | 判断它服务什么具体阅读需要，用材料展开该讲清的关系。 |
| “可能”“仅仅”“不意味着”反复出现 | 连读段组，逐项判断作用，保留必要限定。 |
| 理论被改成一串操作建议 | 补回能够解释措施为何成立的关系。 |
| 文字变顺了，文献、声音或场面却消失了 | 对照实际句段，恢复修改中损失的价值。 |
| 审稿意见语气更保守，就被自动采纳 | 核对意见的位置、依据和影响，再决定如何修改。 |

<p align="center">
  <img src="assets/principles.png" alt="三个核心要求：展开思想，扎根证据，保留声音。" width="100%">
</p>

<a id="quick-start"></a>

## 快速开始

Skill 由 Markdown 指令和参考文件组成，**自身不需要 API Key、依赖包或常驻服务**。实际使用的模型和工具由你的 AI 客户端提供。

### Codex · macOS / Linux

在准备存放仓库的目录中运行：

~~~bash
git clone https://github.com/git-zyyang/anti-defensive-writing.git
cd anti-defensive-writing

# 已有同名安装时保持原状，先比较或备份。
if [ -e "$HOME/.agents/skills/anti-defensive-writing" ] || [ -L "$HOME/.agents/skills/anti-defensive-writing" ]; then
  echo "An installation already exists. Compare or back it up before replacing it."
else
  mkdir -p "$HOME/.agents/skills"
  cp -R skill/anti-defensive-writing "$HOME/.agents/skills/anti-defensive-writing"
fi
~~~

然后在 Codex 中调用：

~~~text
$anti-defensive-writing

请面向学术读者修改下面这段文字，用我提供的材料展开核心解释，
保留引文、研究发现和影响理解的必要条件。
交付改后正文，并简短说明实质性修改。

【粘贴正文和相关依据】
~~~

Codex 官方文档列出的用户级目录为 `~/.agents/skills`，项目级目录为 `.agents/skills`。安装后检查 Skill 选择器；若尚未刷新，重启客户端。[查看 Codex 官方安装路径说明](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills)。

### Claude Code 与其他客户端

Claude Code：将完整的 `skill/anti-defensive-writing` 文件夹复制到 `~/.claude/skills/` 或项目的 `.claude/skills/`，使用 `/anti-defensive-writing` 调用。[查看 Claude Code 官方说明](https://code.claude.com/docs/en/skills#choose-where-skills-load)。

其他客户端使用其文档规定的 Skill 目录。若支持读取文件但不自动发现 Skill，可以明确要求助手读取 `SKILL.md` 和其中链接的表达方法。复制时保留整个 `references` 目录。

这些接入方式依据文件格式和官方路径说明。[验证记录](docs/validation.md)区分了发布包检查、客户端实际运行和模型效果评价。

<a id="examples"></a>

## 改写对照

以下是**附有已知条件的教学示例**，用于展示编辑判断；不是真实研究数据，也不是模型效果对照实验。

### 1. 把已有关系讲出来

**已知条件：**共享词表统一两组团队的术语定义，减少澄清往返。

**原稿**

> 这一小改动或许有所帮助，但不能解决全部协作问题。

**改写**

> 共享词表使两组团队按相同定义理解术语，减少了反复澄清含义的往返沟通。

改后写明了具体变化及其作用。没有交付速度的材料，就不添加“显著提升交付效率”。

### 2. 让表达与证据强度一致

**已知条件：**观察性分析发现正相关，尚无因果识别。

**原稿**

> 这或许可能在一定程度上提示，X可能与Y正相关。

**改写**

> 在该观察性分析中，X与Y呈正相关。

观察性口径仍在，相关关系保持为相关关系。若估计方向或结果本身不确定，仍须表达这种不确定性。

### 3. 必要的限制可以保留

> 样本覆盖三座试点城市，不能据此估计全国普及率。

如果读者可能将结果理解为全国估计，就应保留。摘要独立传播时，即使方法部分已经交代样本，摘要仍可能需要这个条件。

### 4. 人物的犹疑可以有力量

> “我没说要你留下。”他没有关门廊的灯。

在虚构场景中，话语与动作的反差可以承载情绪。改成人物“内心矛盾”的解释，会损失这段文字的体验。

更多案例见[双语教学示例](skill/anti-defensive-writing/references/examples.md)：区分计划与成果、呈现不利结果、保留概念辨析与责任性歉意、判断研究范围、遵守只读请求。

<a id="method"></a>

## 具体怎么判断

### 先发展值得写的内容

明确这段文字要解释、实现或呈现什么，再用材料完成它。构思时比较前人提供了什么基础、当前问题可以推进什么关系。

### 按作用判断限定

遇到一句限定，判断四件事：

1. 它回应哪项具体主张或可能的误解？
2. 当前阅读单元是否已经说明过？
3. 删掉它，读者会失去什么？
4. 它应该进入正文，还是留在修改说明里？

真实的条件、反证、责任、概念区分和人物犹疑都有可能不可缺少。词表只能帮助定位，最终要读懂这句话在做什么。

### 对准实际问题修改

事实错误需要校正；重复可能需要删并；准确却平泛的段落可能需要展开；材料充足却没有重心的段落可能需要重组。已经有解释力和分量的文字应当保留。

### 回到正文判断结果

先放下修改说明，只读改后正文，再对照原文，检查解释、证据、必要条件、理论、声音、节奏与场面。定义和主张改变后，检查相应上下文是否一致。

这些判断融入当前任务，不要求拆成固定调用轮次或审批阶段。完整方法见 [Skill 入口](skill/anti-defensive-writing/SKILL.md)与[共用表达方法](skill/anti-defensive-writing/references/writing-expression.md)。

<a id="scenarios"></a>

## 适用场景

| 写作任务 | 重点 |
|---|---|
| 研究构思、文献讨论 | 比较问题和贡献，再判断是否需要收窄。 |
| 理论论文、专著与教材 | 展开解释，保留引文、理论层次和有依据的判断。 |
| 实证论文 | 解释经过核验的发现，保持与研究设计相符的推断力度。 |
| 基金申报、政策报告 | 连接问题、主体、关系以及拟开展的研究或行动。 |
| 技术说明、商业沟通 | 讲清变化、工作方式和读者需要采取的行动。 |
| PPT、课程和讲稿 | 在屏幕与讲述中合理分配解释，帮助读者理解工作。 |
| 小说与随笔 | 保留欲望、选择、体验、声音和节奏。 |
| 日常消息 | 直接完成沟通，保留必要礼貌与责任。 |

输出语言服从当前请求。公开版运行指令采用英文，README与教学示例提供中英文内容。

<a id="usage"></a>

## 直接可用的调用示例

### 发展研究想法

~~~text
请使用 anti-defensive-writing，帮助发展下面这个研究想法。
结合提供的文献，比较研究问题和解释，
找出值得推进的贡献，并说明需要哪些证据。

研究想法：
已有文献：
现实约束：
~~~

### 修改已有正文

~~~text
请使用 anti-defensive-writing 修改这一节。
用已有材料展开值得解释的关系，
保留引文、必要条件和作者语气。
如有具体证据缺口，放在简短修改说明中指出。
~~~

### 只读审查

~~~text
请使用 anti-defensive-writing 做只读审查。
定位重复设限、无依据收窄，以及此前修改可能损失内容的位置，
说明每项问题的依据和影响。
不要改写正文，也不要修改文件。
~~~

### 精修文学场景

~~~text
请在修改这一场景时使用 anti-defensive-writing。
保留人物声音和有意义的犹疑，
通过已有动作、感知与选择展开体验，
保持既定事件和叙述视角。
~~~

提供读者、文体、材料和必须保护的段落，有助于助手作出具体判断。材料尚缺时，实际取证仍由已授权的研究任务完成。

<a id="integration"></a>

## 接入日常写作流程

安装后，客户端可以发现这个 Skill。若希望在日常写作中持续使用，可以自行将下面一段加入 `AGENTS.md` 或 `CLAUDE.md` 等客户端指令文件：

~~~markdown
自然语言起草与实质审读时，每个任务首次读取 anti-defensive-writing，
将检查融入现有流程。充分展开材料支持的解释，
保留证据、必要条件和作者声音。
遵守只读、纯格式、直接引语和锁定文本的范围。
~~~

这是一项可选配置。仓库不会自动修改指令或安装钩子，具体发现与调用由客户端决定。同一任务复用已读方法，短消息随文检查即可。

<a id="installation"></a>

## 安装、更新与移除

### 项目级安装

Codex：把 `skill/anti-defensive-writing` 复制到项目的 `.agents/skills/`。

Claude Code：复制到项目的 `.claude/skills/`。

保留 `references/` 和随附 `LICENSE`。目标目录已有同名 Skill 时，先检查原有内容。

### Windows

在 GitHub 点击 **Code → Download ZIP**，解压后将 Skill 文件夹复制到用户目录中的对应位置，例如 `%USERPROFILE%\.agents\skills\`。安装后的文件夹应同时包含 `SKILL.md`、`LICENSE` 和 `references`。

### 更新

在仓库副本中运行 `git pull --ff-only`，检查变化，并在替换安装目录前备份个人修改。复制安装的 Skill 不会随仓库拉取自动更新；合并时保留作者自己的定制规则。

### 移除

移除安装的 `anti-defensive-writing` 文件夹，以及自行加入的默认接入指令。若做过个性化修改，先留一份副本。本项目没有需要卸载的后台进程或依赖包。

### 已安装上游同名版本时

本适配版沿用上游 Skill 名称。如果已经安装 Kiterlin 版本，需要明确选择客户端加载哪一份，并处理已有安装；不能假定客户端会合并两份同名规则。

<a id="files"></a>

## 文件结构与验证

~~~text
anti-defensive-writing/
├── README.md                         English guide
├── README.zh-CN.md                   中文说明
├── LICENSE                          保留上游 MIT 声明
├── CONTRIBUTING.md                  双语贡献说明
├── assets/
│   ├── hero.png                     README 封面
│   ├── principles.png               思想／证据／声音主题图
│   └── prompts.md                   图片提示词与生成说明
├── docs/
│   ├── provenance.md                发布包与文档参照
│   └── validation.md                验证范围和评价方法
└── skill/anti-defensive-writing/
    ├── SKILL.md                     可移植入口
    ├── LICENSE                      随安装目录保留许可
    └── references/
        ├── writing-expression.md    共用表达方法
        ├── examples.md              双语教学案例
        └── upstream.md              来源与适配记录
~~~

安装目录自包含。README配图用于展示，不是运行依赖。

发布检查覆盖元数据、相对链接、必要文件、图片可读性，以及本机与私人材料误入发布包的风险。本次发布不提供写作质量的比较基准分数。[验证说明](docs/validation.md)介绍了如何根据实际输出进一步评价效果。

<a id="faq"></a>

## 常见问题

**会不会把话说得过满？**<br>
方法要求表达与证据一致，区分相关与因果、计划与成果、候选解释与核验发现。无依据的确定判断属于需要修正的问题。

**是不是要删掉所有限定？**<br>
影响解释和行动的条件应保留。是否重复、是否必要，要看段落作用，以及摘要或图注是否会被独立阅读。

**会不会把文章越改越短？**<br>
篇幅服从任务。解释太薄时需要展开，重复较多时需要删并；长论证、历史铺陈和场面都可能有价值。

**可以和其他写作或研究 Skill 一起用吗？**<br>
可以。它在原有流程中提供表达判断；研究设计、来源核验、文档排版和交付仍由对应任务负责。

**为什么没有质量评分或“提升百分比”？**<br>
分数本身无法证明论证更有解释力，也无法证明作者声音保住了。本版本提供可检查的判断方法和示例，效果主张需要实际评价记录支持。

<a id="provenance"></a>

## 项目来源

[Kiterlin/anti-defensive-writing](https://github.com/Kiterlin/anti-defensive-writing) 提供上游基础。本适配版进一步贯通构思、起草、审稿裁决、跨文体表达和修改中的价值保护。公开包采用新编教学案例，并移除对维护者私人工作区的依赖。

[来源记录](skill/anti-defensive-writing/references/upstream.md)说明了适配范围和已有基线的文件指纹。README 的组织参考了 [Superpowers](https://github.com/obra/superpowers) 的上手路径、[Anthropic Skills](https://github.com/anthropics/skills) 的自包含目录说明，以及 [Best-README-Template](https://github.com/othneildrew/Best-README-Template) 的导航结构。[文档与图片记录](docs/provenance.md)区分了这些展示参照与 Skill 方法来源。

<a id="contributing"></a>

## 贡献与许可

欢迎通过 [Issues](https://github.com/git-zyyang/anti-defensive-writing/issues) 或 Pull Request 提交具体问题、修改造成的损失案例，或更清楚的解释方法。见[双语贡献指南](CONTRIBUTING.md)。

采用 [MIT 许可](LICENSE)，保留 Kiterlin 的版权声明。本适配版本由 [git-zyyang](https://github.com/git-zyyang) 维护。
