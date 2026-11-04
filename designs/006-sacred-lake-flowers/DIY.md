# DIY 教程：把「神湖花海」改成自己的动态首屏

这条设计的画面主要来自一段全屏视频。只换视频可以改变景色；要让网站成为自己的作品，还需要一起修改封面图、品牌标志、标题和按钮文字。

## 第 1 步：准备三份素材

1. **背景视频：** 选一段横向 MP4。花海湖泊主题可选择花草在前景、湖面在中部、天空在上部的画面。让中央有相对平静的区域，文字才容易读。
2. **静态封面：** 从视频中选一帧，保存为 JPEG。视频尚未加载时，访客会先看到这张图。当前的 `preview.png` 是设计库预览，不能自动充当网页中的视频封面。
3. **品牌标志：** 准备自己的 SVG 或 PNG 标志。原提示词只规定了左上角图片的尺寸，没有提供图片文件。

在 Vite 项目中，可以把文件放在：

```text
public/videos/my-lake.mp4
public/images/hero_bg.jpeg
public/images/my-logo.svg
```

网页引用它们时，路径分别写成 `/videos/my-lake.mp4`、`/images/hero_bg.jpeg` 和 `/images/my-logo.svg`。

## 第 2 步：修改提示词中的视频与封面地址

复制 [原始提示词](prompt.txt)，找到 **Background Video** 中的 `Video URL`，改成自己的视频路径：

```text
Video URL: /videos/my-lake.mp4
Poster image: /images/hero_bg.jpeg
```

提示词在 `index.html` 中还写了两条 preload 链接。图片的 `href` 应与封面路径相同；视频的 `href` 应与新视频路径相同。如果页面已经生成，还要检查 `<video>` 的 `src`、`poster` 和这些 preload 地址是否一致。更换标志时，把导航中的 logo 图片改为 `/images/my-logo.svg`。

> 如果使用外部视频链接，它需要是浏览器能直接播放的视频文件地址。测试时确认链接可访问；如果外部地址失效，把视频放进自己项目的 `public/videos/` 更方便维护。

## 第 3 步：让画面与文字配合

原设计用 `object-cover` 铺满屏幕，因此视频两侧或上下会被裁掉。先在电脑和手机上看一遍：如果湖面或花朵被裁掉，可以调整视频的 `object-position`，例如 `center 60%`；如果主体始终无法保留，换一段构图更合适的视频。

原提示词在视频上放了一层 `bg-black/5` 遮罩。新视频太亮、白色标题难以辨认时，可以在自己的版本中把遮罩加深，例如 `bg-black/20`。调整后再检查花朵与湖面的颜色是否仍然清晰。

## 第 4 步：把太空旅行文案改成自己的主题

原提示词里的 `Venture Past Our Sky Across the Universe`、`Maiden Crewed Voyage to Mars Arrives 2026` 和 `Start Your Voyage` 仍是太空旅行内容。若做花海湖泊主题，可把品牌、导航、消息标签、标题、说明、按钮和底部合作伙伴一起改掉。

你可以在原提示词末尾加上这样的要求，再按自己的业务替换方括号内容：

```text
Use my video at /videos/my-lake.mp4, poster at /images/hero_bg.jpeg, and logo at /images/my-logo.svg. Keep the glass navigation, word-by-word blur-in heading, and two CTA buttons. Change the space-travel copy to a [nature retreat / travel / wellness] theme. Use my brand name [brand], heading [heading], description [description], and CTA labels [primary action] and [secondary action]. Replace the five partner names with [partner names].
```

生成后，让按钮链接到真实页面或操作；只改按钮文字不会自动建立功能。

## 第 5 步：检查动效和手机布局

- 视频是否静音自动播放、循环，并在手机浏览器中正常显示？保留 `autoPlay`、`loop`、`muted`、`playsInline`。
- 视频加载前是否显示同场景的封面？
- 标题逐词出现时，是否有词被裁切或重叠？长中文标题尤其需要检查小屏。
- 导航在手机上是否保留品牌和重要操作入口？
- 白色文字与玻璃按钮在视频明亮的画面上是否仍可辨认？
- 视频和封面是否有权在你的项目中使用？

确认效果后，把新的提示词和预览图保存到自己的条目。这里的原始提示词会保留，方便对照学习。
