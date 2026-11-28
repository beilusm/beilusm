# Material 3 Expressive 动态主页维护

主页复用 [Material You 壁纸工坊](https://github.com/beilusm/material-you-wallpaper) 的几何生成、Monet Expressive 色彩推导、WCAG 对比度校准、SVG 导出和作品分享格式，不依赖额外后端、API Key 或跨仓库写入令牌。

## 自动刷新

`.github/workflows/wallpaper.yml` 每 6 小时运行，约北京时间 04:17、10:17、16:17、22:17。GitHub 的定时任务可能延迟；公开仓库长时间没有活动时，定时任务也可能被停用，可在 Actions 页面重新启用。也可选中 **Refresh profile wallpaper → Run workflow** 手动换图。

工作流只使用本仓库的 `GITHUB_TOKEN` 写入本仓库，读取公开的壁纸仓库。修改壁纸仓库的 `scripts/generate-profile.mjs` 后先推送至壁纸仓库 `main`，随后工作流即会自动采用新版渲染。

每次生成均按当期随机壁纸的色相动态派生浅色与深色两套 Material 3 Expressive 配色，输出：

- `banner-<hash>.svg` / `banner-light-<hash>.svg`：Bento 风格顶部自我介绍与无遮挡生成式壁纸橱窗
- `work-*-{dark,light}-<hash>.svg`：三张连通圆角（Connected Card Group）的代表项目卡片
- `toolkit-{dark,light}-<hash>.svg`：技术栈胶囊与座右铭横条
- `wallpaper-<hash>.svg`：`1600 × 640` 原始无文字壁纸及 `current.json` 参数记录

旧一轮生成的哈希 SVG 会自动从工作区清理，手动放入 `assets/wallpaper/` 的其他文件不受影响。

## 本地换图

需要 Node.js 22 或更新版本，无需安装 npm 依赖：

```bash
node /home/beilusm233/Documents/material-you-wallpaper/scripts/generate-profile.mjs \
  --profile /home/beilusm233/Documents/mygithub/beilusm
```

附加 `--seed 42` 可以复现同一作品。提交 `README.md` 和 `assets/wallpaper/` 后生效。

## 修改介绍与项目

- `README.md` 中 `WALLPAPER:START`..`WALLPAPER:END` 放置顶部 Bento 横幅，`MONET:START`..`MONET:END` 放置随壁纸配色联动的精选项目与技术栈卡片；注释之外可自由增删自定义内容。
- 卡片文案、形状（Cookie / Clover / Sunny Starburst）与配色规则均位于壁纸仓库的 `scripts/generate-profile.mjs`。
