# AI. In sight. — 五种 AI 产品交互

20 秒知识讲解：**适用场景 + 可复用 AI 提示词 + 操作演示**。结尾总结：**场景 + 动作 + 反馈**。

1920×1080 · 60fps · H.264 + AAC。作者署名：[github.com/Jdb156158](https://github.com/Jdb156158)。深色 Bento 布局，紫色、青色、玫红强调；无口播，原创合成配乐与操作音效。

## 视频展示

MP4 与本源码包单独交付，文件名 `ai-microinteractions-20s.mp4`。

![九个关键画面](previews/overview.jpg)

| 时间 | 控件 | 场景 | 操作与反馈 |
|---|---|---|---|
| 0–2s | 五种总览 | AI 产品 | 让过程看得见 |
| 2–5s | 提示词输入 | AI 首页 | 点建议 → 填入 → 发送状态 |
| 5–8s | 流式回答 | 智能助手 | 逐步输出 → 停止 → 保留内容 |
| 8–11s | 引用溯源 | 知识问答 | 悬停编号 → 原句与来源联动 |
| 11–14s | 长文摘要 | 文档阅读 | 扫描重点 → 折叠三条摘要 |
| 14–17s | 图像生成 | AI 绘图 | 噪声渐退 → 选择候选 → 解锁变体入口 |
| 17–20s | 总结 | 场景 + 动作 + 反馈 | 让等待有回应，让结果有来由 |

所有回答、引用、摘要和生成进度均为明确标注的前端示例。图片来自真实摄影素材，不是现场生成。此包交付视频动画源代码，Canvas 中的指针是按时间驱动的操作演示，不是联网 AI 产品。

## 提示词与来源

- [五种完整提示词 + 视频制作提示词](PROMPTS.md)
- [核实记录与时间码分镜](treatment.md)
- 灵感目录：[Lucian UX/UI Prompt](https://lucianlabs.dev/uxui-prompt/)，条目 233、086、224、235、280。本片独立 Canvas 重绘。
- 摄影出处：`assets/photo-sources.json`；字体许可随 `assets/fonts/` 交付。

## 制作步骤

1. 查阅目录与五个原始预览，先提供截图确认选题。
2. 写分镜：每种交互同时提供场景、短提示词和状态变化；完整提示词单独保留。
3. 用 HTML Canvas 绘制。`window.ready` 等待字体和图片，`window.draw(t)` 仅由时间决定，种子噪声可重复，支持任意顺序跳转。
4. 导出九个关键时刻检查。第一轮调整停止状态和来源文字对比度；第二轮提前摘要及选图结果，增加结果停留时间。
5. Python 合成 120 BPM 配乐：2/4 拍，第一拍 0 秒，20 个小节，所有场景切换在小节线。音效随点选、发送、停止、扫描和选图出现。18 秒奏终止和弦，最后 0.8 秒淡出。
6. Playwright 逐帧调用 `draw(i/60)`，生成 1200 张 JPG。
7. ffmpeg 合成 H.264 Main / yuv420p / AAC，规范 BT.709 色彩标记、快速起播并限制音频真峰值。
8. 抽帧总览、确定性回放验证、完整播放及七个时间点跳转检查。

## 在本机复现

需要 Node.js、Python 3（numpy）、ffmpeg，以及 Chrome。不要依赖系统字体，字体已随包提供。

```sh
npm install
python3 -m pip install numpy
python3 make_audio.py
npm run stills
npm run render
sh encode.sh
```

`CHROME_PATH` 可指定 Chrome 路径，默认是 macOS 的 Google Chrome。`FRAME_DIR` 可指定 JPG 输出目录，同时传给渲染与编码脚本。帧序列、可再生 WAV 和 MP4 没有重复放入源码 ZIP。

可直接通过 HTTP 打开 `index.html` 检视动画源文件；安装了 huashu-motion 的机器可运行 `om studio <项目目录>` 获得时间轴预览。
