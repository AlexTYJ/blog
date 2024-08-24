# learning-rate scheduler

## 引言

模型训练到某个阶段，loss会不再下降，而此时学习率改变可能会使得loss进一步降低。因此，动态变化的学习率可能会导致结果变好，我们可以使用pytorch提供的scheduler管理learning rate。一般来说共有六种。

## 详细介绍

### 1 StepLR

$$
new\_ lr = initial\_ lr * \gamma ^{\frac{epoch}{step\_ size}}
$$



```
torch.optim.lr_scheduler.StepLR(optimizer,step_size,gamma=0.1,last_epoch=-1,verbose=False)
```

参数：

- optimizer：模型优化器

- step_size：学习率更新步长

- gamma：衰减率（默认0.1）

- last_epoch ：last_epoch之后恢复lr为initial_lr。使用场景：如果训练了很多个epoch后中断了，继续训练时，这个值就等于加载的模型的epoch。默认为-1，表示从头开始训练，即从epoch=1开始。

- verbose：是否每次改变都输出一次lr的值

示例代码：

```
optimizer = torch.optim.SGD(model.parameters(), lr=0.1, momentum=0.9)
scheduler = StepLR(optimizer, step_size=30, gamma=0.1)

for epoch in range(100):
    train(...)
    validate(...)
    scheduler.step()
```

### 2 MultiStepLR

$$
new\_ lr=initial \_ lr * \gamma ^{bisect\_ right(milestones,epoch)}
$$

```
torch.optim.lr_scheduler.MultiStepLR(optimizer,milestones,gamma=0.1,last_epoch=-1,verbose=False)
```

- optimizer：模型优化器

- milestones 数据类型是递增的list 按设定的间隔调整学习率

- gamma：衰减率（默认0.1）

- last_epoch ：last_epoch之后恢复lr为initial_lr。使用场景：如果训练了很多个epoch后中断了，继续训练时，这个值就等于加载的模型的epoch。默认为-1，表示从头开始训练，即从epoch=1开始。

- verbose：是否每次改变都输出一次lr的值


```
scheduler = MultiStepLR(optimizer, milestones=[30,80], gamma=0.1)

for epoch in range(100):
    train(...)
    validate(...)
    scheduler.step()
```

### 3 MultiStepLR

$$
new\_ lr=initial\_ lr* \gamma ^{epoch}
$$

```
torch.optim.lr_scheduler.ExponentialLR(optimizer,gamma,last_epoch=-1,verbose=False)
```

- optimizer：模型优化器

- gamma：衰减率（默认0.1）

- last_epoch ：last_epoch之后恢复lr为initial_lr。使用场景：如果训练了很多个epoch后中断了，继续训练时，这个值就等于加载的模型的epoch。默认为-1，表示从头开始训练，即从epoch=1开始。

- verbose：是否每次改变都输出一次lr的值

### 4 CosineAnnealingLR

$$
\begin{align*}
new\_ lr &= eta\_ min + \frac{1}{2}(initial\_ lr - eta\_ min)(1+cos(\frac{epoch}{T\_ max}\pi))
$$

- optimizer：模型优化器

- gamma：衰减率（默认0.1）

- eta_min：学习率最小值

- T_max：极值点，当 $epoch<T\_ max$ 时学习率递增，当 $epoch<T\_ max<2epoch$ 时学习率递减。此后做周期性变化直到收敛

- last_epoch ：last_epoch之后恢复lr为initial_lr。使用场景：如果训练了很多个epoch后中断了，继续训练时，这个值就等于加载的模型的epoch。默认为-1，表示从头开始训练，即从epoch=1开始。

- verbose：是否每次改变都输出一次lr的值

```
torch.optim.lr_scheduler.CosineAnnealingLR(optimizer,T_max,eta_min=0,last_epoch=-1,verbose=False)
```

### 5 ReduceLROnPlateau

$$
new\_ lr=\gamma * old\_ lr
$$

```
torch.optim.lr_scheduler.ReduceLROnPlateau(optimizer, mode='min', factor=0.1, patience=10, threshold=0.0001, threshold_mode='rel', cooldown=0, min_lr=0, eps=1e-08, verbose=False)
```

- mode(str)：模式选择
    - min：当指标不再降低(如监测loss)
    - max：表示当指标不再升高(如监测accuracy)。

- factor(float)：学习率调整倍数(等同于其它方法的gamma)，即学习率更新为lr = lr * factor

- patience(int)：忍受该指标多少个step不变化

- verbose：是否每次改变都输出一次lr的值

- threshold(float)配合threshold_mode使用，默认值1e-4。作用是用来控制当前指标与best指标的差异。

- threshold_mode(str)：选择判断指标是否达最优的模式 有两种模式：rel和abs。

    - 当threshold_mode = rel并且mode = max时， $dynamic_threshold = best * ( 1 + threshold )$

    - 当threshold_mode = rel并且mode = min时， $dynamic_threshold = best * ( 1 - threshold )$

    - 当threshold_mode = abs并且mode = max时， $dynamic_threshold = best + threshold$

    - 当threshold_mode = rel并且mode = max时， $dynamic_threshold = best - threshold$

- cooldown(int)：冷却时间。当调整学习率之后，让学习率调整策略冷静一下。模型训练一段时间后再重启监测模式。

- min_lr(float or list)：学习率下限。可为float或者list 当有多个参数组时可用list进行设置。

- eps(float) 学习率衰减的最小值。当学习率变化小于eps时 则不调整学习率。

### 6 LambdaLR
$$
new\_ lr=\gamma * old\_ lr
$$

```
torch.optim.lr_scheduler.LambdaLR(optimizer, lr_lambda, last_epoch=-1)
```

- λ：依参数lr_lambda和epoch得到一个list，分别计算各个parameter groups的学习率更新用到的λ

## 总结
以上六种方法可分为三大类，分别是

1. 依公式有序调整：Step/MultiStep/ Exponential/CosineAnnealing

2. 依训练情况自适应调整：ReduceLROnPlateau

3. 依人为设定自定义调整：Lambda




