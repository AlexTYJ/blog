# 如何使用Tmux远程跑会话

## 原理

一个 tmux 实例可以包含多个**会话（Session）**，一个会话可以包含多个**窗口（Window**），一个窗口可以包含多个**面板（Pane）**。

tmux 会话和其中的进程不直接绑定到启动它们的控制终端。因此，即使控制终端被关闭，由 tmux 管理的会话和进程仍然运行在后台。

## 使用

### 指令

创建新会话：

```bash
tmux new -s <session-name>
```

切换会话：

```bash
tmux switch -t <session-name>
```

分离会话：

```bash
tmux detach
```

列出会话：

```bash
tmux ls
```

关闭会话：

```bash
tmux kill-session -t <session-name>
```

关闭会话的当前窗口：

```bash
exit
```

重连会话：

```bash
tmux a -t session_name 
```

删除会话

```bash
tmux kill-session -t session_name
```

### 快捷键

- 创建新窗口：按下快捷键Ctrl-b，然后按下c。这将在当前会话中创建一个新的窗口

- 切换窗口：按下快捷键Ctrl-b，然后按下数字键0到9，或使用n（下一个）和p（上一个）切换到下一个或上一个窗口

- 重命名窗口：按下快捷键Ctrl-b，然后按下","。这将允许你为当前窗口设置一个新的名称。

- 关闭窗口：按下快捷键Ctrl-b，然后按下&。这将关闭当前窗口

- 拆分窗格：按下快捷键Ctrl-b，然后按下%（垂直拆分）或"（水平拆分）。这将在当前窗口中创建一个新的窗格

- 切换窗格：按下快捷键Ctrl-b，然后按下方向键（上、下、左、右）切换到相邻的窗格

- 调整窗格大小：按下快捷键Ctrl-b，然后按下Alt键加上方向键（上、下、左、右）调整窗格大小

- 关闭窗格：按下快捷键Ctrl-b，然后按下x。这将关闭当前窗格

### 实际操作

1. 创建tmux的session

```bash
tmux new -s <session-name>
```

2. 在tmux下运行程序

3. 分离终端

分离会话：

```bash
tmux detach
```

或者crtl b + d

4. 重新连接tmux

```bash
tmux a -t session_name 
```

5. 删除会话

```bash
tmux kill-session -t session_name
```