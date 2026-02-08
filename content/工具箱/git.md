你以后日常操作 Git 的**基本命令**，其实就围绕这几个循环使用（尤其是个人/小项目开发时）：

### 日常最核心的「工作流」循环（记住这个顺序就够用 80% 的场景）
1. **查看当前状态**（永远先跑这个！）
   ```
   git status
   ```
   → 告诉你：哪些文件改了？有没有需要 commit？当前在哪个 branch？

2. **把改动加到暂存区**（准备提交）
   ```
   git add .          # 加所有改动（最常用）
   # 或
   git add 文件名     # 只加特定文件
   git add src/       # 加某个文件夹
   ```

3. **提交改动**（保存一个版本点）
   ```
   git commit -m "这里写简短说明，比如：修复登录 bug" 
   # 或者多行详细说明：
   git commit -m "修复登录 bug

   详细描述...
   - 改了 login.vue
   - 加了验证逻辑"
   ```

4. **推送到 GitHub**（让别人/云端看到你的更新）
   ```
   git push               # 之后可以直接这样（因为你第一次用了 -u）
   # 第一次推送要写全：
   git push -u origin master   # 或 main，看你的分支名
   ```

5. **从 GitHub 拉最新代码**（多人协作或换电脑时必做）
   ```
   git pull               # 拉取 + 自动合并（最常用）
   # 或分开：
   git fetch              # 只拉更新但不合并
   git merge origin/master
   ```

### 其他超常用命令（几乎每天都会碰到的）
- **创建新分支**（开发新功能时强烈建议，别直接在 master/main 上改）
  ```
  git branch feature-login     # 创建分支
  git checkout feature-login   # 切换过去
  # 合体写法（Git 2.23+ 推荐）：
  git switch -c feature-login
  ```

- **切换分支**
  ```
  git checkout master        # 旧写法
  # 或新写法（推荐）：
  git switch master
  ```

- **查看提交历史**（看自己或别人干了啥）
  ```
  git log                # 完整历史
  git log --oneline      # 简洁版（超好用）
  git log -5             # 只看最近 5 条
  ```

- **撤销/后悔药**（小修小补常用）
  ```
  git restore 文件名          # 丢弃单个文件的改动（回到上次 commit）
  git restore .               # 全部丢弃
  git reset --hard HEAD^      # 回退上一个 commit（危险！小心用）
  ```

### 快速记忆表（打印或贴在桌子上）

| 场景               | 命令                              | 说明                     |
|--------------------|-----------------------------------|--------------------------|
| 检查状态           | `git status`                      | 每天第一件事             |
| 加所有改动         | `git add .`                       |                          |
| 提交               | `git commit -m "消息"`            | 消息要写清楚             |
| 推送               | `git push`                        | 推到 origin 的当前分支   |
| 拉取最新           | `git pull`                        | 先 pull 再开始工作       |
| 新功能开分支       | `git switch -c 新分支名`          | 现代推荐写法             |
| 切换分支           | `git switch 分支名`               |                          |
| 查看历史           | `git log --oneline --graph`       | 加 --graph 更直观        |
| 丢弃改动           | `git restore .`                   | 没 commit 前安全         |

### 小建议（避免以后踩坑）
- 改代码前先 `git pull` → 拉最新避免冲突
- 改完先 `git status` 确认 → 再 add → commit → push
- 提交消息写清楚（英文或中文都行，但要描述做了什么）
- node_modules/、dist/ 等不要 commit（用 .gitignore 挡掉）
- 如果多人协作，建议学一下 `git pull --rebase` 或处理冲突的基本方法

掌握上面这些，你以后操作 Git 基本不会卡住了。  
有具体场景再问我（比如「怎么解决冲突」「怎么删分支」），我可以给你针对性命令～ 加油！