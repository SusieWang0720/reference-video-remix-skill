# Reference Video Remix Skill

Turn a reference video, social post, script, or screenshots into a new product video with structured breakdown, storyboard, generated visuals, licensed background music, voiceover/dialogue, Remotion production, and final render verification.

This is a Codex skill. The actual skill instructions live in [`SKILL.md`](./SKILL.md).

## What It Does

- Breaks down a reference video link or provided frames into pacing, scenes, visual grammar, copy, and audio structure.
- Creates a new original storyboard instead of copying the reference frame-for-frame.
- Generates or organizes scene assets when needed.
- Builds a Remotion video project.
- Adds licensed / royalty-free background music with source and license notes.
- Adds voiceover or scene-specific dialogue.
- Verifies the final MP4 with type checks, render output, `ffprobe`, and still-frame inspection.

## When To Use

Use this skill when you want Codex to create a video like:

```text
Use $reference-video-remix to make a new product video from this reference link.
The product is Tencent RTC Conversational AI. Use licensed background music and female voiceover.
```

You can provide:

- YouTube, X/Twitter, TikTok, or other video links
- spreadsheets or documents with scripts
- screenshots / reference frames
- product brief, CTA, landing page, or brand requirements

## Installation

Clone this repository into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/SusieWang0720/reference-video-remix-skill.git ~/.codex/skills/reference-video-remix
```

Then restart Codex or start a new thread so the skill list refreshes.

## Typical Output Structure

The skill recommends creating a self-contained project folder:

```text
data/video-breakdowns/<slug>/
├── AGENTS.md
├── source/
├── assets/
│   ├── reference/
│   └── generated/
├── notes/
│   ├── breakdown.md
│   ├── storyboard.md
│   └── music-source.md
├── remotion/
└── renders/
```

## Notes

- The skill avoids claiming music is "copyright-free" unless the source explicitly says so.
- It records music title, artist, source URL, license wording, local asset paths, and restrictions.
- If a reference video is blocked by login or anti-bot checks, the skill records exactly what was verified and what remained unresolved.
- It is intended to be used together with Remotion, image generation, browser inspection, and spreadsheet/document skills when available.

---

# Reference Video Remix Skill（中文）

把一个参考视频、社交平台视频链接、脚本或截图，拆解并制作成一个新的产品视频。流程包括：参考视频拆解、脚本和分镜、场景图生成、Remotion 制作、授权背景音乐、配音/场景对白，以及最终渲染验证。

这是一个 Codex skill。实际的执行说明在 [`SKILL.md`](./SKILL.md)。

## 它能做什么

- 拆解参考视频的节奏、分镜、画面语言、文案结构和音频结构。
- 基于参考做原创视频，不逐帧复制原视频。
- 需要时生成或整理场景图、产品图和视觉素材。
- 创建 Remotion 视频项目并完成成片。
- 查找并使用有授权依据的免版税 / 可商用背景音乐。
- 添加完整旁白，或只在特定场景中加入客服/角色对白。
- 用类型检查、Remotion 渲染、`ffprobe` 和抽帧检查验证最终 MP4。

## 什么时候使用

当你想让 Codex 根据一个参考链接或脚本制作类似产品视频时使用，例如：

```text
使用 $reference-video-remix，根据这个视频链接做一个新的产品介绍视频。
产品是 Tencent RTC Conversational AI，需要有授权背景音乐和女声配音。
```

你可以提供：

- YouTube、X/Twitter、TikTok 或其他视频链接
- 带脚本的 Excel / Word / 文档
- 截图或参考帧
- 产品介绍、CTA、落地页、品牌要求

## 安装方式

把仓库 clone 到 Codex skills 目录：

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/SusieWang0720/reference-video-remix-skill.git ~/.codex/skills/reference-video-remix
```

然后重启 Codex，或开启一个新线程，让 skill 列表刷新。

## 推荐输出结构

skill 会建议为每个视频项目创建独立目录：

```text
data/video-breakdowns/<slug>/
├── AGENTS.md
├── source/
├── assets/
│   ├── reference/
│   └── generated/
├── notes/
│   ├── breakdown.md
│   ├── storyboard.md
│   └── music-source.md
├── remotion/
└── renders/
```

## 注意事项

- 不会随便把音乐说成“无版权”，除非来源页面明确这么写。
- 会记录音乐标题、作者、来源链接、license 说明、本地路径和限制条件。
- 如果参考视频被登录、反爬或地区限制挡住，会明确记录已验证内容和 unresolved 部分。
- 适合和 Remotion、图像生成、浏览器检查、表格/文档处理等能力一起使用。
