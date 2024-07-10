# LAMMPS 时间估算器使用说明

## 简介
`lammps_time_estimator.py` 是一个用于估算 LAMMPS 模拟运行时间的 Python 程序。它通过读取 `log.lammps` 文件中的循环时间数据和输入文件中的总步数，计算出在相同核心数下运行整个模拟所需的时间。

## 先决条件
- 安装了 Python 3.x
- LAMMPS 已经运行并生成了 `log.lammps` 文件
- LAMMPS 的输入文件命名为 `in.*`（例如 `in.input`）

## 使用方法

### 1. 准备工作
确保以下文件在当前工作目录中：
- `log.lammps`：包含 LAMMPS 运行日志
- `in.*`：包含 LAMMPS 输入的文件，例如 `in.input`

### 2. 下载或创建脚本
下载或复制代码保存为 `lammps_time_estimator.py`

### 3. 运行脚本

#### 默认使用方式
在终端或命令行中运行以下命令：
```sh
python lammps_time_estimator.py
```
此命令将自动查找当前目录中的 `log.lammps` 文件和以 `in.` 开头的输入文件。

#### 指定文件和步数
你也可以指定 `log.lammps` 文件和输入文件，或者直接指定总步数：
```sh
python lammps_time_estimator.py -l log.lammps -i in.input -s 500000
```
s
### 4. 查看结果
脚本将输出读取到的 `loop time`，`procs` 和 `steps` 信息，并显示估算的总运行时间。例如：
```
Extracted: Loop time = 0.764362s, Procs = 30, Steps = 67
Estimated time for 500000 steps: 5.10 hours (assuming the same number of processors: 30)
```

## 注意事项
- 请确保 `log.lammps` 文件和输入文件的路径正确。
- 脚本假设所有 `Loop time` 行中的 `procs` 数量相同。
- 输出的估算时间是在相同核心数的前提下计算的。

## 常见问题
**Q: 如果输入文件中有多个 `run` 命令，如何处理？**
A: 脚本会自动累加所有 `run` 命令中的步数。

**Q: 如果我有多个 `Loop time` 行，如何计算？**
A: 脚本会读取所有的 `Loop time` 行，并计算平均每步的时间以估算总时间。
