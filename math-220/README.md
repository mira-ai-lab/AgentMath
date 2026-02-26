# AgentMath：Math-220

## 🎯 数据集简介

该数据集旨在模拟实际场景中复杂多样的数学答疑环境，包含文本、符号、图像、语音、视频等多模态输入，涵盖代数、几何、算术、证明、应用题、概率统计、微积分、组合问题、应用数学、图论以及逻辑等11个类型，共220条高质量样本。

## 🗂️ 目录结构

```
math-220/
│
├── audio-220/
│   ├── 16.mp3
│   ├── 17.mp3
│   └── ...
│
├── img-220/
│   ├── 9.png
│   ├── 11.jpg
│   └── ...
│
├── video-220/
│   ├── 6.mp4
│   ├── 7.mp4
│   └── ...
│
└── dataset-220.json
```

## 📑 数据格式

| 字段 | 类型 | 说明 | 示例 |
|---|---|---|---|
| `id` | Integer | 每个样本的唯一标识符。 | `1` |
| `task_domain` | String | 任务所属的数学领域，例如：代数（algebra）、几何（geometry）、证明（proof）、逻辑（logic）等。 | `"algebra"` |
| `input_modality` | String | 输入模态类型，例如：`text_only`、`text_image`、`image_audio`、`video_only` 等。 | `"image_audio"` |
| `problem_text` | String | 题目的文本描述，支持使用 LaTeX 表示数学公式。 | `"Compute $\sum_{n=1}^\infty \dots$"` |
| `problem_image` | List[String] | 题目关联的图像文件列表；如果没有图像输入，则为空列表 `[]`。 | `["11.jpg"]` |
| `audio_file` | String / NaN | 题目关联的音频文件（`.mp3`）；如果不存在则为 `NaN` 或 `null`。 | `"16.mp3"` |
| `video_file` | String / NaN | 题目关联的视频文件（`.mp4`）；如果不存在则为 `NaN` 或 `null`。 | `"6.mp4"` |
| `final_answer` | Mixed | 问题的最终答案，可以是数字、字符串或 LaTeX 表达式。 | `"2"`、`"19"`、`"$\frac{\pi}{12}$"` |
| `reasoning_steps` | String / NaN | 详细的解题推理过程（Step-by-step reasoning）。 | `"Because $y = \dots$"` |
