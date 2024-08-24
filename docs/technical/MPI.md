# MPI:Message Passing Interface

Message Passing Interface，即「消息传递接口」，指的是多进程并行时不同进程之间通信的**协议**或**标准**


```
from mpi4py import MPI

# 初始化 MPI 环境
MPI.Init()

# 获取全局通信器
comm = MPI.COMM_WORLD

# 获取当前进程的编号和进程总数
rank = comm.Get_rank()
size = comm.Get_size()

# 只有主进程发送消息
if rank == 0:
    for i in range(1, size):
        message = f"Hello from rank 0 to rank {i}"
        comm.send(message, dest=i)
        print(f"Rank 0 sent message to Rank {i}")
else:
    # 其他进程接收来自主进程的消息
    message = comm.recv(source=0)
    print(f"Rank {rank} received message: {message}")

# 结束 MPI 环境
MPI.Finalize()

```

该代码输出：

```
Rank 0 sent message to Rank 1
Rank 0 sent message to Rank 2
Rank 0 sent message to Rank 3
Rank 1 received message: Hello from rank 0 to rank 1
Rank 2 received message: Hello from rank 0 to rank 2
Rank 3 received message: Hello from rank 0 to rank 3
```

其中包括了六个常用函数：

- Init : 表示使用MPI的部分开始

- Finalize : 表示使用MPI的部分结束

- comm.Get_rank() : 返回执行当前代码的进程号

- comm.Get_size() : 确定进程数

- comm.send(obj,dest,tag) : 发送一条消息

    - obj：要发送的数据对象。可以是任何可序列化的 Python 对象，例如字符串、数字、列表、字典等。
    
    - dest：目标进程的编号（rank），即消息要发送到哪个进程。

    - tag（可选）：消息的标签，用于标识消息的类型或内容。默认值为 0。

- comm.recv(source,tag,status) : 接收一条消息

    - source（可选）：消息的源进程编号（rank），即从哪个进程接收消息。可以设置为特定的进程编号，或者使用 MPI.ANY_SOURCE 接收来自任何源的消息。
    
    - tag（可选）：消息的标签，用于过滤接收特定标签的消息。可以设置为特定的标签值，或者使用 MPI.ANY_TAG 接收任何标签的消息。

    - status（可选）：一个 MPI.Status 对象，用于获取接收到消息的状态信息，例如源进程编号、标签等。


