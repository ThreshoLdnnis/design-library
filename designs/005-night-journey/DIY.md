# DIY 教程：把「星夜兼程」改成自己的夜景首屏

这条设计主要由一段全屏视频、顶部导航和居中的标题组成。原提示词没有额外的装饰层，因此换视频时，画面的明暗与构图会直接影响文字是否清晰。

## 第 1 步：准备视频和静态封面

选择横向视频，尽量让天空或留白出现在上半部，人物、建筑等主体位于下半部。这样标题可以放在较安静的画面上。再准备一张与视频相近的静态图片，供视频加载前显示。

如果使用 Vite 项目，可以放在：

```text
public/videos/night-scene.mp4
public/images/night-poster.jpg
```

网页中相应的路径是 `/videos/night-scene.mp4` 和 `/images/night-poster.jpg`。当前目录的 [`preview.png`](preview.png) 是用户提供的设计封面，并不是可播放的视频。

## 第 2 步：替换视频地址

复制 [原始提示词](prompt.txt)，找到 **Video Background** 中的 `Source URL`，改为自己的直接视频地址：

```text
Source URL: /videos/night-scene.mp4
Poster image: /images/night-poster.jpg
```

原文没有指定 `poster`，第二行是可以补充的要求。如果网页已经生成，也要在 `<video>` 元素中把 `src` 与 `poster` 改成相同路径，并保留 `autoPlay`、`loop`、`muted` 和 `playsInline`。

## 第 3 步：调整裁切和文字可读性

原视频使用 `object-cover` 铺满屏幕。新视频若把人物或关键景物裁掉，可以改变 `object-position`，或选择主体更适合横屏的视频。

原提示词要求不加装饰图形、径向渐变和额外遮罩，因此最好优先挑选上半部较暗、细节较少的视频。如果白色标题被明亮画面淹没，可以改用更合适的视频画面；如需加深视频或加遮罩，应在修改后的提示词中明确说明这个变化。

## 第 4 步：替换品牌与文案

把 `Velorah®`、导航栏目、标题、说明文字和两个 `Begin Journey` 按钮改成你的真实品牌内容。若仍保留标题中部分词语的灰色强调，要重新指定哪些词使用 `<em>` 样式。

例如，换成夜间阅读主题时，可以要求：

```text
Keep the full-screen starry video and glass navigation. Change the brand to my reading project, rewrite the heading for quiet nighttime reading, and change both CTA labels to "Explore the Library". Keep the three staggered fade-rise animations.
```

导航链接和按钮也应指向真实页面或操作，而不只是展示文案。

## 第 5 步：统一字体和间距

原文同时写了 `Instrumental Serif` 与 `Instrument Serif`。制作页面时，选定一种字体，并让 Google Fonts 导入地址、CSS 变量和标题的 `fontFamily` 保持一致。

首屏容器同时列出 `pt-32`、`pb-40` 和 `py-[90px]`。如果实际留白不符合预期，明确选择一套上、下内边距，分别检查桌面与手机尺寸。标题在手机上较长时，也要确认不会超出屏幕。

## 第 6 步：检查效果

- 视频加载前是否有合适的静态封面？
- 视频每个亮度变化的画面上，标题与按钮是否清晰？
- 手机屏幕上导航、标题和按钮是否完整可见？
- 两个行动按钮是否通向正确的位置？
- 视频循环时是否出现明显跳帧？

确认后，把新的提示词、封面和视频放进自己的设计条目。
