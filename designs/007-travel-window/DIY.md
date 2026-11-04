# DIY 教程：把「旅行窗外」改成自己的动态首屏

这条设计的列车窗框和远景来自背景视频。换一段视频，就能改变窗外经过的景色；如果想换成飞机或轮船的窗户，素材中也要有对应的窗框，或额外制作窗框图层。

## 第 1 步：选视频并截取封面

选一段横向 MP4，让画面的中央窗户足够宽、景色相对平静，以便放置标题和输入框。尽量避免快速闪动、强烈曝光变化或窗框遮住文字。再从视频中截取一张静态封面，供视频加载前显示。

在 Vite 项目中，可以放在：

```text
public/videos/my-window.mp4
public/images/my-window-poster.jpg
```

页面中对应的路径是 `/videos/my-window.mp4` 和 `/images/my-window-poster.jpg`。设计库的 [`preview.png`](preview.png) 只是预览图，不会自动成为网页视频的封面。

## 第 2 步：替换提示词中的视频地址

复制 [原始提示词](prompt.txt)，找到 **Background** 下的 `Video URL`，改成自己的地址，并明确加上封面要求：

```text
Video URL: /videos/my-window.mp4
Poster image: /images/my-window-poster.jpg
```

如果页面已经生成，也要更新 `<video>` 的 `src` 和 `poster`。保留 `autoPlay`、`loop`、`muted` 和 `playsInline`，再在手机上实际检查自动播放。原提示词还要求预加载；若项目里已有视频 preload 地址，记得同步修改，避免预加载旧视频。

## 第 3 步：调整窗景裁切与文字对比

视频使用 `object-cover` 时，会随屏幕比例裁掉部分画面。先检查桌面和手机：窗框是否完整、地平线是否落在合适位置、主体是否被标题挡住。如果裁切不理想，试着调整 `object-position`，或换一段更适合竖屏的视频。

原设计用近黑色标题和灰色正文，适合明亮天空。换成夜景后，可以把标题和说明改成浅色；白天景色过亮或过杂时，适当调整遮罩、文字阴影或视频取景。输入框的强模糊和半透明黑底，也要在新画面上检查可读性。

## 第 4 步：替换品牌、文案和按钮

把 `http://Railroad.ai`、导航栏目、`10K+ already subscribed`、主标题、说明文字、`Get Started` 与 `Join Waitlist` 改成自己的内容。订阅人数应使用真实数字；没有数据时，换成不含数字的说明。按钮应链接到真实页面或操作。

可以在原始提示词末尾加入自己的修改要求，例如：

```text
Use /videos/my-window.mp4 as the background video and /images/my-window-poster.jpg as its poster. Keep the window-view composition, glass navigation, and staggered blur-in animations. Replace the Railroad.ai brand with [my brand], change the heading to [my heading], and rewrite the description for [my product]. Change the two buttons to [primary action] and [waitlist action].
```

如果你希望「加入候补名单」真的保存邮箱，需为表单接入服务或后端接口，并添加提交成功、失败和邮箱格式错误的反馈；只有输入框外观不会自动保存数据。

## 第 5 步：确定字体并检查手机布局

原提示词要求导入 Instrument Serif 和 Barlow，却又指定标题与正文实际使用系统字体。若想保持预览图中的效果，可以直接使用系统字体；若想改成衬线标题，要同步更新字体样式，并重新检查标题的换行和宽度。

完成前检查：

- 视频加载前是否出现正确的静态封面？
- 窗框在桌面和手机上是否没有被裁到影响观感？
- 标题、说明和邮件输入框在视频播放过程中是否始终清楚？
- 逐词动画是否顺畅，长标题在手机上是否完整？
- 邮件提交和两个行动按钮是否有实际功能？

确认后，把更新后的提示词、预览图和自己使用的视频素材保存到条目中。
