## 搞懂 git-rebase

### 起因

项目管理中，突然发现 许多重复描述 的 commit 以及存在大量无用的提交

### 导致问题

- 不利于代码 `review`
- 会造成分支的污染

### 使用场景一 ：合并多次 提交记录

1. 合并最近4次的提交记录，执行：

   ```bash
   git rebase -i HEAD~4
   ```

2. 这时候，会自动进入 `vi` 编辑模式：

   ```bash
   s cacc52da add: qrcode
   s f072ef48 update: indexeddb hack
   s 4e84901a feat: add indexedDB floder
   s 8f33126c feat: add test2.js
   
   # Rebase 5f2452b2..8f33126c onto 5f2452b2 (4 commands)
   #
   # Commands:
   # p, pick = use commit
   # r, reword = use commit, but edit the commit message
   # e, edit = use commit, but stop for amending
   # s, squash = use commit, but meld into previous commit
   # f, fixup = like "squash", but discard this commit's log message
   # x, exec = run command (the rest of the line) using shell
   # d, drop = remove commit
   #
   # These lines can be re-ordered; they are executed from top to bottom.
   #
   # If you remove a line here THAT COMMIT WILL BE LOST.
   #
   # However, if you remove everything, the rebase will be aborted.
   #
   ```

   

