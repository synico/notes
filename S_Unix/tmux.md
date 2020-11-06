## Tmux

### 会话
#### 新建会话
```
tmux new -s <session-name>
```
#### 查看会话
```
tmux ls
tmux list-session
```
#### 接入会话
```
tmux attach -t <session-name>
```
#### 杀死会话
```
tmux kill-session -t <session-name>
```
#### 切换会话
```
tmux switch -t <session-name>
```
#### 重命名会话
```
tmux rename-session -t <session-name> <new-name>
```
#### 快捷键
* 分离当前会话

```
Ctrl + b d
```
* 列出所有会话

```
Ctrl + b s
```
* 重命名当前会话

```
Ctrl + b $
```

### 窗格操作
#### 划分窗格
* 划分上下两个窗格

```
tmux split-window
```
* 划分左右两个窗格

```
tmux split-window -h
```

#### 移动光标
* 光标切换到上方窗格
```
tmux select-pane -U
```

* 光标切换到下方窗格
```
tmux select-pane -D
```

* 光标切换到左边窗格
```
tmux select-pane -L
```

* 光标切换到右边窗格
```
tmux select-pane -R
```

#### 交换窗格位置
* 当前窗格上移
```
tmux swap-pane -U
```

* 当前窗格下移
```
tmux swap-pane -D
```

