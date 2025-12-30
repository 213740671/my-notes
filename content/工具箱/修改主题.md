# Quartz（GitHub Pages + Actions）下次换主题的注意事项（备忘）

## 1. 你现在的部署方式
- 你用的是 **GitHub Actions** 构建 + GitHub Pages 发布
- workflow 监听分支：`v4`（只有 push 到这个分支才会触发部署）

## 2. 换主题最核心：改 THEME_NAME
在 `.github/workflows/*.yml` 里（通常是 `build` job 下）找到：

```yml
env:
  THEME_NAME: xscriptor
```

把 `xscriptor` 改成你想要的主题名即可，例如：

```yml
env:
  THEME_NAME: tokyo-night
```

> 主题名一般就是 quartz-themes 仓库 `themes/` 目录下的文件夹名。

## 3. 拉主题的步骤必须在 build 之前
确保 workflow 中顺序是：

1) `npm ci`  
2) **Fetch Quartz Theme（拉主题）**  
3) `npx quartz build`  
4) upload artifact → deploy

示例（关键步骤）：

```yml
- name: Fetch Quartz Theme
  run: curl -s -S https://raw.githubusercontent.com/saberzero1/quartz-themes/master/action.sh | bash -s -- $THEME_NAME
```

## 4. 提交后如何验证是否生效
- 去 GitHub 仓库的 **Actions** 页面确认最新一次 workflow 成功
- 等 Pages 更新后刷新浏览器（必要时强刷：Ctrl+F5 / Cmd+Shift+R）

## 5. 常见“换了没效果”的原因排查
1) **推错分支**：workflow 只监听 `v4`，你如果 push 到别的分支不会部署  
2) **浏览器缓存**：强刷或清缓存再看  
3) **自定义样式覆盖**：`quartz/styles/custom.scss` 里如果写了很多 CSS/SCSS，可能把主题样式盖掉  
4) **主题是单一模式**：只有深色或只有浅色的主题，切换按钮会导致显示怪

## 6. 单一模式主题的额外处理（可能需要）
如果主题只有“纯深色/纯浅色”，通常要移除暗黑切换组件：
- 打开 `quartz.layout.ts`
- 找到 `Component.Darkmode()` 并删除/注释掉

## 7. 你改主题时建议的最小改动策略
- 首先只改 `THEME_NAME` 测试主题效果
- 确认满意后，再少量在 `custom.scss` 做微调（比如字体、行距、链接样式）
- 尽量避免在 `custom.scss` 写大段“全局覆盖”，否则以后换主题会更容易冲突

## 8. 备份建议（不想翻车的话）
- 每次换主题前先 commit 一次当前状态
- 换完主题确认无误再 commit（这样随时可以回滚）
