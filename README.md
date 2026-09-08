# 个人主页

单页静态站，无构建步骤、无依赖。改内容只动 `index.html`。
设计沿用 Jon Barron 的版式（视觉/机器人圈的惯例），页脚已按惯例署了来源。

## 状态

**已上线**：<https://zzh18877220541.github.io>
仓库 `zzh18877220541/zzh18877220541.github.io`，public，Pages 从 `main` 分支根目录发布。
两版 CV 的 `\homepage{}` 已启用。

## 更新

```bash
cd homepage && git add -A && git commit -m "..." && git push
```

推送后 Pages 自动重新构建，约 30 秒生效。

### 注意：SSH 走 443 端口

remote 用的是 `ssh://git@ssh.github.com:443/...` 而不是常规的 `git@github.com:...`，
因为当前网络下 GitHub 的 22 端口不通（`ssh -T git@github.com` 会 `Connection closed`）。
443 这条是 GitHub 官方提供的备用通道。换网络后两者都能用，不必改回去。

想让所有仓库都走这条，可以在 `~/.ssh/config` 里把 github.com 那段改成：

```
Host github.com
  HostName ssh.github.com
  Port 443
  User git
  IdentityFile ~/.ssh/id_rsa
```

## 图

现有两个真实素材：

| 文件 | 内容 | 来源 |
| --- | --- | --- |
| `images/portrait.jpg` | 证件照 | 本人提供 |
| `images/motus2.mp4` | *Find Square* 记忆探针 demo，2.2 MB | Motus2 项目页 `assets/video/demos/find_square_1.mp4` |

选 Find Square 而不是别的 demo，是因为记忆机制正是简历里主张 owner 的那一块，
视频和文字互相印证；换成 `screw_bulb` 之类就只是「一个机器人 demo」，说明不了你的贡献。

其余条目**故意没有配图**，做成纯文本全宽。灰色占位框会让页面看起来没做完，
而只有第一条带视频、其余纯文本是一种成立的版式。想补图就在 `.meta` 前面插回：

```html
<div class="thumb">
  <img src="images/xxx.jpg" alt="...">
  <p class="caption">可选说明</p>
</div>
```

值得补的，按优先级：

1. **麻将 VLA 真机 demo** —— 目前没有录像（在面壁那边）。这是全站最可惜的缺口：
   一个双臂机器人打真人麻将的动图，说服力远高于任何文字描述。能要到就要。
2. **ScaleEdit 的替换前后对比** —— 一组 before/after 最能说明「物理尺寸错误」这个问题，
   而且这是你唯一完全独立的工作，值得可视化。
3. EruDiff teaser 图、TLS-Cache 架构图 —— 从论文里截即可，优先级最低。

动图控制在 5 MB 以内。单文件上限是 100 MB，但加载慢会直接劝退访客。
长视频用 `<video src="..." autoplay loop muted playsinline>`，
`.entry .thumb video` 的样式已经写好（含 300 px 高度上限）。

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
