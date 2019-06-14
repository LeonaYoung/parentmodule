## Parent Module

### User A 首次在 parent module 中添加子模块

```bash
git submodule add https://github.com/LeonaYoung/submodule.git
git commit -m 'add submodule'
git push
```

### User B 克隆已经添加了子模块的 parent module

```bash
git clone https://github.com/LeonaYoung/parentmodule.git
git submodule init
# 注册子模块
git submodule update
# clone 子模块
```

**注意**

在拥有子模块的仓库中，多人开发非子模块的部分，和普通仓库开发没有差异

### 子模块内部有了更新，parent module 中对其拉新

子模块有更新，父模块没法感知，除非进入子模块路径下

```bash
git fetch 
git pull

# 然后回到parentmodule根路径下，这点非常重要，不要忘记

cd .. && git status 

# 后会发现有未提交的修改 modified:   submodule (new commits)
# 记得拉新完子模块的代码，一定要立即提交推送到远端；以便于其他用户不用再进入子模块去更新代码；
git add 
git commit
git push
```

### 接下来是 User B 的操作

在 parent module 的根路径下执行

```bash
git fetch
git pull
# 会看到 submodule | 2 +-
git status
# 会看到 modified:   submodule (new commits)
git submodule update
git status
# 这时才会看到 working tree clean，此时userB才完成了sunmodule 的更新；
```

### 在父模块中更新子模块

为啥要做这种操作呢？直接去子模块仓库中改代码不好吗？

```bash
cd submodule

# do some change

git add
git commit 
git push

# 注意虽然是在 parentmodule 中操作的修改，但这次提交记录是在 submodule 中的；

cd ..
git status

# 会看到 modified:   submodule (new commits)，和之前一样，需要继续下面步骤

git add
git commit
git push

# 这一次提交就是在parentmodule 中了
```

#### 然后 userB 又要去拉新啦

```bash
git pull
git submodule update
```
