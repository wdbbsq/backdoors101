# 服务器训练

[TensorBoard 官方教程](https://pytorch.org/docs/stable/tensorboard.html)

## 映射转发端口

```shell
ssh -L 16006:127.0.0.1:6006 root@192.168.2.136
```

## tensorboard

```shell
cd /root/zsq/backdoor101/

source activate zsq_backdoor101

tensorboard --logdir=runs/
```

[tensorboard 地址](http://127.0.0.1:16006/#scalars)


# 本地训练

```shell
conda info --env

conda create --name [ENV_NAME] python=3.9

canda activate [ENV_NAME]

conda remove -n [ENV_NAME] --all
```

## tensorboard

```shell
conda activate backdoor101
```

```shell
tensorboard --logdir=D:/FederatedBullshit/backdoors101/runs
```

# 调用流程

```python
import metrics.metric
import tasks.task
import training
import helper

# 主函数入口，解析yaml文件，初始化任务信息
helper = helper.Helper()
task = tasks.task.Task()
metrix = metrics.metric.Metric()

# 开始训练
training.fl_run()

# epoch start
# 1. 执行训练任务
training.run_fl_round()
# 2. 测试当前模型性能
training.test()
# 2.1 保存到TensorBoard文件中
task.report_metrics()
metrix.plot()
# 3. 按需保存当前模型参数
helper.save_model()


```