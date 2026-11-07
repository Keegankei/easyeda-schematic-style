# EasyEDA Schematic Style

[English](README.md) | **简体中文**

一套用于绘制和整理 **EasyEDA 专业版原理图**的可复用智能体技能。它帮助智能体采用参考图页的视觉风格或工程默认设置，同时保留电气设计，并在用户指定的范围内进行编辑。参考图页不是必需条件。

本技能包提供操作说明和参考指南，不包含 MCP 服务器、EasyEDA 扩展或器件库。

## 功能范围

- 按功能划分区域，让信号流向清晰易读。
- 紧凑、清晰地呈现现有外围电路的局部接线。
- 统一标题、器件位号、参数值和网络标签的格式。
- 根据实际连接生成跨图页接口汇总。
- 对比网表、检查视觉布局，并保护只读图页。
- 检查 API 状态，并根据当前版本核对编辑方式。

本技能侧重原理图的组织与呈现。PCB 布线、器件选型和电气设计变更需要另行明确任务范围。

## 使用条件

- 支持 `SKILL.md` 技能，或能够按要求读取这些说明的智能体。
- 能够访问相关 EasyEDA 专业版工程；参考图页可选。
- 若需自动编辑，须已有可用的官方 EasyEDA MCP、CLI 或扩展 API 连接，以及对应安装版本的文档。

安装本技能不会自动安装或配置 EasyEDA 连接。本技能包仅包含文档，无需 Python 依赖包或附带运行环境。

## 安装

### Codex：选择安装位置

选择一种安装范围，将**完整的** `easyeda-schematic-style` 文件夹复制到对应位置。需要跨工程复用时，使用用户级目录比较方便。以下路径依据 [Codex 官方本地技能文档](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills)。

| 安装范围 | 技能文件夹位置 |
|---|---|
| Windows，当前用户 | `%USERPROFILE%\.agents\skills\easyeda-schematic-style\` |
| macOS / Linux，当前用户 | `~/.agents/skills/easyeda-schematic-style/` |
| 当前工程 | `<project-root>/.agents/skills/easyeda-schematic-style/` |

`%USERPROFILE%` 和 `~` 表示当前用户的主目录，`<project-root>` 表示在 Codex 中打开的工程根目录。这些都是通用路径，不对应某个人的本机目录。使用 WSL 或远程环境时，应使用 Codex 实际运行环境中的用户主目录。

Windows 用户可以在文件资源管理器中打开 `%USERPROFILE%`，依次创建 `.agents` 和 `skills` 文件夹（如果尚不存在），再把技能文件夹粘贴到 `skills` 中。若仅供当前工程使用，则在工程内创建 `.agents/skills`。

### 文件放置示例

复制完成后，入口文件应位于 `<skills-directory>/easyeda-schematic-style/SKILL.md`：

```text
<skills-directory>/
└── easyeda-schematic-style/
    ├── SKILL.md
    ├── README.md
    ├── README.zh-CN.md
    ├── CONTRIBUTING.md
    ├── LICENSE
    ├── .gitignore
    ├── .gitattributes
    └── references/
        ├── schematic-style-guide.md
        └── easyeda-api-notes.md
```

例如，Windows 用户级安装的入口为 `%USERPROFILE%\.agents\skills\easyeda-schematic-style\SKILL.md`。解压 ZIP 后，注意不要多套一层同名的 `easyeda-schematic-style` 文件夹。`references/` 应与 `SKILL.md` 同级，不能只复制入口文件。

### 确认识别并开始使用

Codex 通常会自动发现技能变化；若未出现，请重启 Codex。在 Codex CLI 或 IDE 扩展中，可使用 `/skills` 或输入 `$` 查找 `easyeda-schematic-style`，再在请求中加入 `$easyeda-schematic-style`。详见 [官方技能调用说明](https://learn.chatgpt.com/docs/build-skills#how-chatgpt-and-codex-use-skills)。

其他兼容智能体请使用各自支持的技能目录和调用方式，也可以让其直接读取 [SKILL.md](SKILL.md)，并指定工程和允许编辑的图页。安装本技能提供的是绘图指导；自动编辑 EasyEDA 仍需具备“使用条件”中所述的连接。

## 没有参考图页时如何开始

无需先准备参考图页，也不需要自己确定字体和字号。告诉智能体允许编辑哪张图页，并要求采用内置通用风格指南和工程默认设置即可。它会：

- 按功能整理现有电路，并添加清晰的分区标题。
- 整理信号流向和局部接线，让连接关系易于阅读。
- 使用当前可用字体，统一位号、参数值和网络标签的呈现。
- 保留现有电气连接、器件和接地拓扑。

可以直接复制下面的请求，将 `Controller` 替换为实际图页名：

```text
使用 $easyeda-schematic-style 整理 Controller 图页。
我没有参考图页，请采用通用风格指南和工程默认设置。
优化功能分区、局部接线的呈现方式和标注可读性。
保留当前位号、参数值、封装、装配属性、网络和 NC 标记。
仅修改此图页。保存后核对连接关系，说明修改内容和已完成的检查。
```

如果想先了解修改思路，可以要求先检查并提出布局建议，不进行编辑。如果图页还是空白的，应先提供计划使用的器件和连接关系，或另行明确电路设计任务。缺少视觉参考可以采用默认格式；缺少电路需求则应列出待补充信息，不凭空编造。

## 使用示例

### 沿用已有图页的风格

```text
使用 $easyeda-schematic-style 整理 Controller 图页的格式。
将 Interface 图页作为只读的风格参考。
保留所有器件、参数值、封装、网络和 NC 标记。
不要修改任何 PCB 或其他板卡。
```

### 添加接口汇总

```text
为 Power 图页添加不参与电气连接的接口汇总。
根据当前工程提取网络名称和连接去向。
保持现有电路和布局不变。
```

### 仅检查，不修改

```text
使用 $easyeda-schematic-style 检查选定的原理图图页。
指出标签重叠、局部接线不清晰和格式不一致的问题。
不要修改工程。
```

以上图页名称仅用于示例，请替换为实际工程中的名称和操作范围。

## 工作流程

1. 确认允许编辑的图页、已有的只读参考图页和受保护对象。
2. 获取最新原生数据、渲染视图及修改前的电气基线。
3. 提取合适的视觉层级，整理授权范围内的内容。
4. 保存并重新读取，对比连接关系，检查新导出的图页。
5. 说明修改内容、已完成的检查和仍待解决的问题。

本技能保留当前工程对 DNP（不装配）器件、测试点、接地拓扑和编号的既有约定。它不会自动生成审核签名，也不会仅凭 API 调用成功就认定原理图正确。

## 文件结构

```text
easyeda-schematic-style/
├── SKILL.md
├── README.md
├── README.zh-CN.md
├── CONTRIBUTING.md
├── LICENSE
├── .gitignore
├── .gitattributes
└── references/
    ├── schematic-style-guide.md
    └── easyeda-api-notes.md
```

| 文件 | 用途 |
|---|---|
| [English README](README.md) | 本说明的英文版本 |
| [SKILL.md](SKILL.md) | 智能体入口，定义范围、流程和核对要求 |
| [原理图风格指南](references/schematic-style-guide.md) | 布局、接线呈现、标注和接口汇总 |
| [EasyEDA API 注意事项](references/easyeda-api-notes.md) | 对象标识、坐标、状态处理和 API 核对 |
| [贡献指南](CONTRIBUTING.md) | 改进建议及可复现问题报告的提交要求 |

技能入口、参考指南和贡献指南目前使用英文。

## 参与贡献

请阅读 [CONTRIBUTING.md](CONTRIBUTING.md)。使用虚构示例，避免在提交内容中包含实际工程文件、访问凭据、个人路径或私有设计信息。

## 作者

KeeganKei

## 许可证

本技能包采用 [MIT 许可证](LICENSE)。
