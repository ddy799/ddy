# Agent Skills

个人使用的 Agent Skills 集合。每个技能都是独立目录，含 `SKILL.md`（入口）与 `references/`（按需加载的细节），可直接拷到 Agent Skills 宿主目录使用。

## 目录

| 技能 | 用途 |
|---|---|
| [`lawgpt`](skills/lawgpt/) | 知识引导式法律文书生成（起诉状/答辩状/上诉状/代理词/律师函/法律意见书/申请书） |

## 安装

### WorkBuddy

```bash
cp -r skills/<name> ~/.workbuddy/skills/
```

### Claude Code / 其他 Agent Skills 宿主

```bash
cp -r skills/<name> ~/.claude/skills/
```

技能按需加载：宿主只读 `SKILL.md`，其余 `references/` 在触发后按提示读取。新装技能需新开一轮会话才会进入技能列表。

## lawgpt

把 LaWGPT（南京大学 LAMDA，2023）的 Knowledge-based Self-Instruct 数据合成思路迁移到文书起草：**先造要素表，再让正文只能从表里取料**。

四阶段流水线：

1. **Grounding** — 抽七栏要素表（主体/法律关系/请求/要件事实/时间轴/证据/管辖）
2. **Skeleton** — 套法定骨架，不凭感觉分段
3. **Realization** — 分段成稿，每段只取表内材料
4. **Cleaning** — 三道闸自检：事实可回溯、条号可核验、要素齐备

设计要点：

- 交稿必须附「待补清单」，列明缺失要素、无证据断言、待核验条号
- 条号分两类：**已核验基线**（民诉法 2023 修正第 122/124/128/171/172 条，经北大法宝核对）与**基线外现查**，禁止凭记忆引用
- 宁缺条号，不造假条号

### 边界

产出为**草稿**，不是法律意见。署名、出具、提交前须执业律师核签。不虚构证据、不虚构条号、不虚构当事人信息。

### 来源与许可

`lawgpt` 技能本体为本仓库原创内容。其中 `references/lawgpt-method.md` 记录的是第三方开源项目 [pengxiao-song/LaWGPT](https://github.com/pengxiao-song/LaWGPT)（GPL-3.0）的公开事实与引用，不含其代码或模型权重；该项目仅供学术研究、严禁商业用途、严禁用于真实法律场景，本技能不复现也不部署该模型，仅借用其方法论。

法条原文引用自北大法宝，条文著作权归相应立法机关，此处仅作指引与核验记录。
