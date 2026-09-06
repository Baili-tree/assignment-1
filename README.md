# assignment-1

一个用于学习 **Agent、大模型上下文（LLM Context）、Skill** 三个核心概念的教学练习仓库，同时演示「项目级 Skill」从创建、调用到产出的完整工作流。

## 仓库用途

1. **概念学习**：通过自定义 Skill「概念学习资料生成器」生成结构化的概念学习资料
2. **Skill 实践**：演示如何在项目仓库中创建、存放和调用一个项目级 Skill
3. **知识沉淀**：产出的学习资料与概念关系文档可作为后续复习与分享的材料

## 仓库结构

```
assignment-1/
├── README.md                          # 本文件
├── concept-relationship.md            # 三个概念的关系说明（含 Mermaid 图）
├── learning-materials/                # 学习资料产出目录
│   ├── Agent-学习资料.html
│   ├── LLM-Context-学习资料.html
│   └── Skill-学习资料.html
└── .workbuddy/
    └── skills/
        └── 概念学习资料生成器/
            └── SKILL.md               # 项目级 Skill 定义
```

## Skill 存放路径

**项目级 Skill 路径**：

```
.workbuddy/skills/概念学习资料生成器/SKILL.md
```

说明：

- 项目级 Skill 存放在**仓库根目录**的 `.workbuddy/skills/<skill-name>/SKILL.md`，仅对本项目（及其协作者）生效
- 与之相对，用户级 Skill 存放在 `~/.workbuddy/skills/`，跨项目可用；本仓库采用项目级，便于随仓库分发
- `SKILL.md` 顶部使用 `---` 包围的 YAML 元数据（`name`、`description`），这是 Skill 被识别与索引的依据

## Skill 是什么、怎么调用

「概念学习资料生成器」Skill 定义了生成学习资料的**七模块模板**：

1. 学习目标（可检验的行为目标）
2. 核心问题（直指概念本质）
3. 结构化解释（定义、要点、机制、来龙去脉、前置知识）
4. 应用案例（生活类比 + 真实场景 + 反例）
5. 概念辨析（易混淆概念对照 + 误解纠正）
6. 自测题（附答案解析，覆盖学习目标形成闭环）
7. 参考来源（只列真实出处，禁止编造文献）

**调用方式**：在以本仓库为工作空间的 AI 助手对话中，直接用自然语言触发，例如：

```
帮我学习 XXX 概念
生成 XXX 的学习资料
```

助手识别到任务与 Skill 的 `description` 匹配后，会自动加载 SKILL.md，按模板一次性产出完整学习资料。生成结果默认为 Markdown，本次应用户要求输出为 HTML 并存入 `learning-materials/`。

## 生成了哪些资料

| 文件 | 内容概要 |
|------|----------|
| `learning-materials/Agent-学习资料.html` | 以"感知—思考—行动"循环（ReAct）为核心，讲解 Agent 四大组成（大脑/规划/记忆/工具），辨析 Agent vs Chatbot vs Workflow vs LLM |
| `learning-materials/LLM-Context-学习资料.html` | 用"工作台桌面"类比讲解上下文窗口、Token、注意力平方级开销，辨析四种信息来源，破除"窗口大就该全塞进去"的误区 |
| `learning-materials/Skill-学习资料.html` | 拆解 SKILL.md 五个组成部分（元数据/触发条件/工作流程/输出模板/质量准则），辨析 Skill vs Prompt 模板 vs Memory vs MCP vs Agent |
| `concept-relationship.md` | 用 Mermaid 图和两两辨析表说明三个概念的关系：Skill 决定"往上下文放什么"，上下文决定"Agent 此刻知道什么"，Agent 决定"用这些知识做什么" |

三份学习资料均遵循 Skill 的质量闭环要求：核心问题在后文解释中得到回答、自测题覆盖学习目标、误解条目与辨析模块呼应、参考来源只列真实可查的出处。

## 核查与修改过程

本仓库的构建经历了以下实际过程，记录于此以备回顾：

### 1. 仓库克隆与环境踩坑

- 首次克隆 GitHub 仓库时，因 bash 调用原生 git.exe 的路径转换问题，仓库被误克隆到 `C:\d\assignment-1`
- **核查**：通过 PowerShell 的 `Test-Path` 与目录列表比对 D 盘实际内容，发现 D 盘并无该目录
- **修正**：确认误建目录仅含刚克隆的 `.git` 后将其清理，改用 Windows 路径格式（`D:/assignment-1`）重新克隆，成功落盘 `D:\assignment-1`
- GitHub 直连不稳定（时通时断），克隆经过多次重试才成功

### 2. Skill 创建

- 在仓库根目录创建 `.workbuddy/skills/概念学习资料生成器/SKILL.md`
- 按 Skill 规范编写：YAML 元数据（`name`、`description`）+ 七模块工作流程 + 输出模板 + 质量准则（防幻觉、闭环校验、语言跟随）
- **核查**：写入后通过 `ls` 和 `head` 验证文件已正确落盘

### 3. 学习资料生成与自检

- 按用户要求依次调用该 Skill 生成三份资料（Agent / LLM Context / Skill），输出为 HTML
- 每份资料生成后对照 Skill 内置质量准则自检：
  - ✅ 七个模块齐全，顺序与模板一致
  - ✅ 核心问题在后文"结构化解释"中有明确回应
  - ✅ 自测题覆盖全部学习目标（学习目标 → 自测题映射闭环）
  - ✅ "常见误解"条目与"概念辨析"模块相互呼应
  - ✅ 参考来源仅列真实可查的出处（书籍、经典论文、官方文档），未编造链接；无法确认的内容标注"待核实"
- **核查**：生成完毕后列出 `learning-materials/` 目录，确认三个文件全部就位

### 4. 概念关系文档

- `concept-relationship.md` 用两张 Mermaid 图（分层协作图 + 时序图）和三组两两辨析表，说明 Agent、LLM Context、Skill 的关系
- 强调关键洞察：Skill 不是独立程序，它必须被加载进上下文才能生效——三者构成"知识资产 → 信息空间 → 行动主体"的分层协作系统

### 5. 我的核查和修改

我阅读了 AI 生成的所有内容，把其中过于技术化的表述改成了更易懂的说法，比如把"上下文窗口"类比成"短期记忆"。同时我核实了所有参考来源链接，确认都是真实可查的。另外，我在三个概念的学习资料中都补充了自己的理解，让内容更贴近个人学习风格。

## 使用建议

- 若要为其他概念生成学习资料，直接在对话中说"帮我学习 X 概念"即可
- 若要修改资料风格，编辑 `.workbuddy/skills/概念学习资料生成器/SKILL.md` 中的输出模板部分
- `learning-materials/` 中的 HTML 文件可直接用浏览器打开阅读
