## dataset

dataset可以创建数据集


```
from torch.utils.data import Dataset


class ImageDataset:
    def __init__(self, raw_data):
        self.raw_Data = raw_data
    
    def __len__(self):
        return len(self.raw_Data)
    
    def __getitem__(self, index):
        image, lable = self.raw_Data[index]
        return image, lable


```

## dataloader

dataloader加载、划分数据集

```
dataset = face_dataset # Dataset部分自定义过的face_dataset # 创建Dateset(可以自定义)
    
dataloader = torch.utils.data.DataLoader(dataset,batch_size=64,shuffle=False,num_workers=8)  # Dataset传递给DataLoader

for i in range(epoch):
    for index,(img,label) in enumerate(dataloader):    # DataLoader迭代产生训练数据提供给模型
        ........
```

关于dataloader的参数：

```
DataLoader(dataset, batch_size=1, shuffle=False, sampler=None,
           batch_sampler=None, num_workers=0, collate_fn=None,
           pin_memory=False, drop_last=False, timeout=0,
           worker_init_fn=None)
```

- num_workers (python:int, optional): 多少个子程序同时工作来获取数据，多线程。 (default: 0)

- collate_fn (callable, optional): 合并样本列表以形成小批量。

- pin_memory (bool, optional): 如果为True，数据加载器在返回前将张量复制到CUDA固定内存中。

- drop_last (bool, optional): 如果数据集大小不能被batch_size整除，设置为True可删除最后一个不完整的批处理。如果设为False并且数据集的大小不能被batch_size整除，则最后一个batch将更小。(default: False) 

- timeout (numeric, optional): 如果是正数，表明等待从worker进程中收集一个batch等待的时间，若超出设定的时间还没有收集到，那就不收集这个内容了。(default: 0) 

- worker_init_fn (callable, optional*):每个worker初始化函数 (default: None)

