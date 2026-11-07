<h1 align="center">EasyEDA Schematic Style</h1>

<p align="center">
  <strong>原理图清晰易读，风格统一。</strong><br>
  面向 EasyEDA 专业版的布局、标注与核对技能。
</p>

<p align="center">
  <a href="README.md">English</a> · <strong>简体中文</strong>
</p>

<p align="center">
  <a href="https://github.com/Keegankei/easyeda-schematic-style/releases/tag/v1.0.0"><img src="assets/badges/version.svg" alt="版本 1.0.0"></a>
  <a href="SKILL.md"><img src="assets/badges/format.svg" alt="格式：Codex 技能"></a>
  <a href="LICENSE"><img src="assets/badges/license.svg" alt="许可证：MIT"></a>
</p>

**版本 1.0.0** · [发布说明](https://github.com/Keegankei/easyeda-schematic-style/releases/tag/v1.0.0) · [下载 ZIP](https://github.com/Keegankei/easyeda-schematic-style/releases/download/v1.0.0/easyeda-schematic-style-v1.0.0.zip)

[开始使用](#get-started) · [功能](#features) · [示例](#examples) · [核对](#verification) · [指南](#guides) · [许可证](#license)

---

一套用于绘制、整理和检查 **EasyEDA 专业版原理图**的可复用智能体技能。采用参考图页的视觉风格或工程默认设置，同时保留电气设计，并在授权范围内进行编辑。

> **参考图页可选。** 从已有电路和图页名称开始即可；技能内的指南提供布局与文字排版原则。

<a id="get-started"></a>

## 开始使用

### 1. 确认使用条件

- 支持 `SKILL.md` 技能，或能够按要求读取这些说明的智能体。
- 能够访问相关 EasyEDA 专业版工程；参考图页可选。
- 若需自动编辑，须已有可用的官方 EasyEDA MCP、CLI 或扩展 API 连接，以及对应安装版本的文档。

本技能包提供操作说明和参考指南，不包含 MCP 服务器、EasyEDA 扩展或器件库。安装技能不会配置 EasyEDA 连接。技能包本身无需 Python 依赖包或附带运行环境。

### 2. 下载并安装

**[下载 easyeda-schematic-style-v1.0.0.zip](https://github.com/Keegankei/easyeda-schematic-style/releases/download/v1.0.0/easyeda-schematic-style-v1.0.0.zip)**

解压 ZIP 后，将**完整的** `easyeda-schematic-style` 文件夹复制到下列**一个**位置。需要跨工程复用时，选择用户级目录。

| 安装范围 | 技能文件夹位置 |
|---|---|
| Windows，当前用户 | `%USERPROFILE%\.agents\skills\easyeda-schematic-style\` |
| macOS / Linux，当前用户 | `~/.agents/skills/easyeda-schematic-style/` |
| 当前工程 | `<project-root>/.agents/skills/easyeda-schematic-style/` |

这些路径依据 [Codex 官方本地技能文档](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills)。`%USERPROFILE%` 和 `~` 表示当前用户的主目录；`<project-root>` 表示在 Codex 中打开的工程根目录。使用 WSL 或远程环境时，应使用 Codex 实际运行环境中的用户主目录。

Windows 用户可以在文件资源管理器中打开 `%USERPROFILE%`，依次创建 `.agents` 和 `skills` 文件夹（如果尚不存在），再把技能文件夹粘贴到 `skills` 中。若仅供当前工程使用，则在工程内创建 `.agents/skills`。

入口文件应位于 `<skills-directory>/easyeda-schematic-style/SKILL.md`。例如，Windows 用户级安装的入口为 `%USERPROFILE%\.agents\skills\easyeda-schematic-style\SKILL.md`。`references/` 应与 `SKILL.md` 同级，不能只复制入口文件。解压 ZIP 后，注意不要多套一层同名的 `easyeda-schematic-style` 文件夹。

### 3. 发出第一个请求

Codex 通常会自动发现技能变化；若未出现，请重启 Codex。在 Codex CLI 或 IDE 扩展中，可使用 `/skills` 或输入 `$` 查找 `easyeda-schematic-style`，再在请求中加入 `$easyeda-schematic-style`。详见 [官方技能调用说明](https://learn.chatgpt.com/docs/build-skills#how-chatgpt-and-codex-use-skills)。

其他兼容智能体请使用各自支持的技能目录和调用方式，也可以让其直接读取 [SKILL.md](SKILL.md)，并指定工程和允许编辑的图页。自动编辑 EasyEDA 仍需具备上述连接。

**没有参考图页？** 采用通用风格指南和工程默认设置即可，无需自己确定字体和字号。智能体可以整理现有电路的功能分区、局部接线与标注，同时保留器件、电气连接和接地拓扑。

可以直接复制下面的请求，将 `Controller` 替换为实际图页名：

```text
使用 $easyeda-schematic-style 整理 Controller 图页。
我没有参考图页，请采用通用风格指南和工程默认设置。
优化功能分区、局部接线的呈现方式和标注可读性。
保留当前位号、参数值、封装、装配属性、网络和 NC 标记。
仅修改此图页。保存后核对连接关系，说明修改内容和已完成的检查。
```

**想先了解修改思路？** 可以要求先检查并提出布局建议，不进行编辑。

**从空白图页开始？** 请先提供计划使用的器件和连接关系，或另行明确电路设计任务。缺少视觉参考可以采用默认格式；缺少电路需求则应列出待补充信息，不凭空编造。

<a id="features"></a>

## 功能

| 类别 | 指导内容 |
|---|---|
| **布局** | 功能分区、清晰的信号流向、分区标题和一致的间距。 |
| **连接** | 紧凑呈现现有外围电路的局部接线，根据实际连接整理跨图页接口汇总。 |
| **标注** | 统一器件位号、参数值、网络标签和接口去向的呈现。 |
| **核对** | 对比网表、检查新导出图页、保护只读图页，并根据安装版本检查 API 状态。 |

<a id="examples"></a>

## 更多使用示例

<details>
<summary><strong>沿用已有图页的风格</strong> — 使用只读风格参考</summary>

```text
使用 $easyeda-schematic-style 整理 Controller 图页的格式。
将 Interface 图页作为只读的风格参考。
保留所有器件、参数值、封装、网络和 NC 标记。
不要修改任何 PCB 或其他板卡。
```

</details>

<details>
<summary><strong>添加接口汇总</strong> — 说明当前跨图页连接</summary>

```text
为 Power 图页添加不参与电气连接的接口汇总。
根据当前工程提取网络名称和连接去向。
保持现有电路和布局不变。
```

</details>

<details>
<summary><strong>仅检查，不修改</strong> — 汇总布局问题</summary>

```text
使用 $easyeda-schematic-style 检查选定的原理图图页。
指出标签重叠、局部接线不清晰和格式不一致的问题。
不要修改工程。
```

</details>

以上图页名称仅用于示例，请替换为实际工程中的名称和操作范围。

<a id="verification"></a>

## 编辑范围与核对

1. 确认授权编辑的图页、只读参考图页和受保护对象。
2. 获取最新原生数据、渲染视图及修改前的电气基线。
3. 根据参考图页或通用指南，整理授权范围内的内容。
4. 保存并重新读取，对比连接关系，检查新导出的图页。
5. 说明修改内容、已完成的检查和仍待解决的问题。

仅整理格式时，保留当前位号、器件参数值、封装、NC 状态和装配属性，并沿用工程对 DNP（不装配）器件、测试点、接地拓扑和编号的既有约定。参考图页及受保护对象保持不变；技能不会自动生成审核签名，也不会仅凭 API 调用成功就认定原理图正确。

本技能侧重原理图的组织与呈现。PCB 布线、器件选型和电气设计变更需要另行明确任务范围。

<a id="guides"></a>

## 指南与文件

| 文件 | 用途 |
|---|---|
| [SKILL.md](SKILL.md) | 智能体入口，定义范围、流程和核对要求 |
| [原理图风格指南](references/schematic-style-guide.md) | 布局、接线呈现、标注和接口汇总 |
| [EasyEDA API 注意事项](references/easyeda-api-notes.md) | 对象标识、坐标、状态处理和 API 核对 |
| [贡献指南](CONTRIBUTING.md) | 改进建议及可复现的问题报告 |
| [English README](README.md) | 本说明的英文版本 |

技能入口、参考指南和贡献指南目前使用英文。

<details>
<summary><strong>查看完整文件结构</strong></summary>

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
    ├── assets/
    │   └── badges/
    │       ├── version.svg
    │       ├── format.svg
    │       └── license.svg
    └── references/
        ├── schematic-style-guide.md
        └── easyeda-api-notes.md
```

</details>

## 参与贡献

请阅读 [CONTRIBUTING.md](CONTRIBUTING.md)。使用虚构示例，避免在提交内容中包含实际工程文件、访问凭据、个人路径或私有设计信息。

---

<a id="license"></a>

## 作者与许可证

版权所有 © 2026 **KeeganKei**。本技能包采用 [MIT 许可证](LICENSE)。
