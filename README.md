# 个人主页

单页静态站，无构建步骤、无依赖。改内容只动 `index.html`。
设计沿用 Jon Barron 的版式（视觉/机器人圈的惯例），页脚已按惯例署了来源。

## 部署

GitHub Pages 要求仓库名必须等于 `<用户名>.github.io`，否则不会作为个人主页发布。

```bash
cd homepage
git init -b main
git add -A
git commit -m "Personal homepage"
git remote add origin git@github.com:zzh18877220541/zzh18877220541.github.io.git
git push -u origin main
```

推完到 GitHub 仓库的 **Settings → Pages**，Source 选 `Deploy from a branch`，
分支 `main`、目录 `/ (root)`。首次发布约 1 分钟，地址是
<https://zzh18877220541.github.io>。

上线后把 `cv/main.tex` 与 `cv/main-zh.tex` preamble 里的 `\homepage{}` 取消注释。

## 待替换的图

`images/` 下六个 `.svg` 都是占位图，尺寸对了但内容是灰框。换成同名文件即可，
`index.html` 不用改（换成 `.gif` / `.png` / `.jpg` 时记得改 `src` 的扩展名）。

| 文件 | 放什么 | 备注 |
| --- | --- | --- |
| `portrait.svg` | 证件照或半身照 | 竖版，约 5:6 |
| `motus2.svg` | Motus2 真机 demo | **优先做这个**，最好是循环 GIF |
| `mahjong.svg` | 麻将 VLA 真机 demo | 同上，动图比静图有力得多 |
| `erudiff.svg` | 论文 teaser 图 | 直接从论文里截 |
| `tlscache.svg` | 架构图 | 同上 |
| `scaleedit.svg` | 替换前后对比 | 一组 before/after 最能说明问题 |

动图控制在 5 MB 以内，GitHub Pages 单文件上限 100 MB 但加载慢会直接劝退访客。
需要放长视频就用 `<video src="..." autoplay loop muted playsinline>` 替掉 `<img>`，
CSS 里 `.entry .thumb video` 已经写好样式了。

## 本地预览

```bash
cd homepage && python3 -m http.server 8000
```

然后开 <http://localhost:8000>。也可以直接双击 `index.html`，相对路径同样能用。

## 内容同步

正文信息（论文列表、经历、教育）都是从 `cv/main.tex` 搬过来的。
改简历时如果动到这些，记得回来同步一次，别让两处说法不一致。
`cv.pdf` 是 `cv/main.pdf` 的副本，简历改完重新拷一份：

```bash
cp cv/main.pdf homepage/cv.pdf
```
