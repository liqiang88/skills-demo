# skills-demo

Agent Skills 示例仓库，用于演示如何编写、组织与试用最小可用的 Skill。

## 项目简介

Agent Skills 是通过 `SKILL.md` 向 Agent 注入特定任务流程、输出格式与领域知识的 Markdown 能力包。本仓库提供可直接对照学习的示例，帮助你快速理解 Skill 的结构与触发方式。

## 目录结构

```text
skills-demo/
├── README.md
└── examples/
    ├── hello-world/         # 最小 Skill 示例（问候语）
    │   └── SKILL.md
    └── roll-dice/           # 掷骰子：用终端命令生成随机数
        └── SKILL.md
```

| 路径 | 说明 |
|------|------|
| `examples/` | 示例 Skill 集合 |
| `examples/hello-world/` | Hello World 演示 Skill |
| `examples/roll-dice/` | 掷骰子演示 Skill（终端随机数） |

## 示例：hello-world

路径：[`examples/hello-world/SKILL.md`](examples/hello-world/SKILL.md)

这是一个最小 Skill，演示固定格式问候：

- **触发场景**：用户说 hello world、要问候演示，或想试用最小 Skill
- **行为**：只回复一行，格式为 `Hello, {name}!`（未给名字时用 `World`）
- **`disable-model-invocation: true`**：关闭模型自动调用，适合作为手动/显式演示

示例对话：

| 用户 | Agent |
|------|--------|
| hello world | `Hello, World!` |
| hello runoops | `Hello, runoops!` |

## 示例：roll-dice

路径：[`examples/roll-dice/SKILL.md`](examples/roll-dice/SKILL.md)

演示通过**终端命令**生成随机数来掷骰子，而不是由模型自己编造数字：

- **触发场景**：用户说掷骰子、roll dice、`2d6` / `d20` 等
- **行为**：用 `python -c "…random.randint…"`（或 PowerShell `Get-Random`）出结果并简短回复
- **默认**：`1d6`；支持 `NdM` 多骰与求和
- **`disable-model-invocation: true`**：适合显式 `@roll-dice` 演示

## 如何试用

Skill 需要放到 Agent 可加载的技能目录后才会生效。本仓库的 `examples/` 是示例源码，可按需复制到下列位置之一：

| 类型 | 路径约定 | 作用范围 |
|------|----------|----------|
| 个人 Skill | 用户配置目录下的 `skills/<skill-name>/` | 对本机所有项目可用 |
| 项目 Skill | 仓库内项目级 `skills/<skill-name>/` | 仅当前仓库（可随仓库共享） |

试用 `hello-world` 示例：

1. 将 `examples/hello-world` 复制到个人或项目的技能目录，并保持目录名为 `hello-world`
2. 在 Agent 对话中发送 `hello world` 或 `hello <你的名字>`
3. 观察回复是否符合 Skill 规定的格式

试用 `roll-dice` 示例：

1. 将 `examples/roll-dice` 复制到个人或项目的技能目录，并保持目录名为 `roll-dice`
2. 在 Agent 对话中 `@roll-dice` 或发送「掷骰子」「roll 2d6」
3. 确认 Agent 先跑终端命令再给出点数

> 注意：不要把自定义 Skill 写入由内置能力占用的系统技能目录。

## Skill 基本结构

每个 Skill 是一个目录，至少包含 `SKILL.md`：

```text
skill-name/
├── SKILL.md       # 必需：YAML frontmatter + 指令正文
├── reference.md   # 可选：详细参考
├── examples.md    # 可选：更多示例
└── scripts/       # 可选：辅助脚本
```

`SKILL.md` 典型形态：

```markdown
---
name: your-skill-name
description: >-
  简要说明做什么、何时使用。
disable-model-invocation: true   # 可选：禁止模型自动调用
---

# Your Skill Name

## Instructions

1. ...
```

要点：

- **`name`**：Skill 标识
- **`description`**：决定 Agent 何时选用该 Skill，写清能力与触发场景
- **正文**：给出可执行的步骤、格式与边界（少做/不做的事也要写清）

## 新增示例建议

在 `examples/` 下新建目录，保持「一个 Skill 一个文件夹」：

1. 创建 `examples/<skill-name>/SKILL.md`
2. 写好 frontmatter 的 `name` 与 `description`
3. 在正文中给出清晰步骤与输入/输出示例
4. 在本 README 的「目录结构」与示例列表中补充一行说明

## 许可

示例代码仅供学习与演示使用。
