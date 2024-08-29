## DDP

直接给出示例代码：

```
import torch
import torch.distributed as dist
import argparse #用于解析命令行参数

parser = argparse.ArgumentParser() # 创建一个解析器对象
parser.add_argument("--local_rank", default=-1) # 添加 local_rank 参数，用于指定当前进程在本地的 GPU 编号
FLAGS = parser.parse_args() # 解析命令行参数并存储在 FLAGS 中
local_rank = FLAGS.local_rank # 获取 local_rank 参数的值

torch.cuda.set_device(local_rank) # 设置当前进程要使用的 GPU 设备，local_rank 对应的是该进程使用的 GPU 编号
dist.init_process_group(backend='nccl')  # 指定通信后端为NCCL

device = torch.device("cuda", local_rank) # 创建一个表示当前设备的 CUDA 设备对象
model = nn.Linear(10, 10).to(device) # 创建一个线性模型并将其移动到当前设备上
model = DDP(model, device_ids=[local_rank], output_device=local_rank) # 将模型包装为DDP

outputs = model(torch.randn(20, 10).to(rank)) # 随机输入，获取输出
labels = torch.randn(20, 10).to(rank) # 生成随机label
loss_fn = nn.MSELoss() #创建loss
loss_fn(outputs, labels).backward() #反向传播

optimizer = optim.SGD(model.parameters(), lr=0.001) #优化器
optimizer.step() #优化器

```

Bash运行：

```
# 使用torch.distributed.launch启动DDP模式，其会给main.py一个local_rank的参数
python -m torch.distributed.launch --nproc_per_node 4 main.py
```