- 每天写代码以前，先 `PULL` 再开发
- 提交控制工具依赖 [commitizen](https://github.com/commitizen/cz-cli)
    - `git cz` 提交
    ```
    feat：新功能（feature）
    fix：修补bug
    docs：文档（documentation）
    style： 格式（不影响代码运行的变动）
    refactor：重构（即不是新增功能，也不是修改bug的代码变动）
    test：增加测试
    chore：构建过程或辅助工具的变动 
    ``` 
- 提交时按逻辑相关性，无关的修改不要一起提交
    - 修复一个 bug，提交一次，修复另一个 bug 再提交一次
- 开发一个功能时，有另外一个 bug 要修正，使用 `git stash`
    - 先 `git stash`
    - [切换分支]修复 bug ，提交
    - [切换回来原分支]再 `git stash pop`，接着之前的工作，完成这个功能，再 commit
- 分支提交次数小的时候，快速合并用 `cherry-pick`
    - [切换分支]提交修改的东西，`git log` 可以拿到提交记录
    - 切到 [master] `git cherry-pick xxx` 即可