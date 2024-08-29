# launch.json 

下面是一个示例

```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "languagemodel debug",
            "type": "debugpy",
            "request": "launch",
            "cwd": "/hpc_stor03/sjtu_home/yujie.tu/research/deeplearning_course_sjtu/languagemodel",
            "program": "main.py",
            "console": "integratedTerminal",
            "args": [
                "--data","data/gigaspeech",
                "--cuda",
                "--epochs","6"
            ],
            "python":"/hpc_stor03/sjtu_home/yujie.tu/miniconda3/envs/languagemodel/bin/python"
        }
    ]
}
```

TIPS：

- cwd是工作区位置，一定要设置，否则import自己写的文件的时候可能出问题

- program是执行文件，是相对于cwd的位置

- python是虚拟环境中pyhton解释器的位置，可以用绝对路径