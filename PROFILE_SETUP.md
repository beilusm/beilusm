# 随机壁纸维护

主页横幅复用 [Material You 壁纸工坊](https://github.com/beilusm/material-you-wallpaper) 的几何生成、SVG 导出和作品分享格式，不依赖额外后端、API Key 或仓库间写入令牌。

## 自动刷新

`.github/workflows/wallpaper.yml` 每 6 小时运行，约北京时间 04:17、10:17、16:17、22:17。GitHub 的定时任务可能延迟；公开仓库长时间没有活动时，定时任务也可能被停用，可在 Actions 页面重新启用。也可选中 **Refresh profile wallpaper → Run workflow** 手动换图。

工作流只使用本仓库的 `GITHUB_TOKEN` 写入本仓库，读取公开的壁纸仓库。先将壁纸仓库的 `scripts/generate-profile.mjs` 推送到 `main`，再发布本仓库工作流。

每次提交生成一张 SVG 横幅、一张不带文字的原始 SVG 壁纸及 `assets/wallpaper/current.json` 参数记录；旧的生成文件会从当前目录移除，Git 历史仍保留。图片文件名随内容变化，以减少图片缓存旧图。图片及文字链接打开完全相同的造型、颜色、尺寸和种子；横幅上的文字和暗色遮罩仅用于主页，不属于导出的原始作品。为支持无浏览器的生成，随机作品不启用颗粒纹理。

## 本地换图

需要 Node.js 22 或更新版本，无需安装 npm 依赖：

```bash
node /home/beilusm233/Documents/material-you-wallpaper/scripts/generate-profile.mjs \
  --profile /home/beilusm233/Documents/mygithub/beilusm
```

附加 `--seed 42` 可以复现同一作品。提交 `README.md` 和 `assets/wallpaper/` 后生效。

## 修改介绍

自由修改 `README.md` 中 `WALLPAPER:START` 和 `WALLPAPER:END` 注释之外的内容。任务仅替换两条注释之间的自动生成区域。

字体、标题和横幅排版在壁纸仓库的 `scripts/generate-profile.mjs` 中调整。首次因设置限制写入失败时，检查本仓库 Actions 的工作流令牌是否允许写入，以及 `main` 是否受分支保护规则限制。
