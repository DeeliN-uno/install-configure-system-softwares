# VSC使用ANACONDA终端虚拟环境踩坑记录

## 1. ANACONDA设置

### 1. 创建虚拟环境

`conda create -n Materials` 创建一个名为材料的虚拟环境

### 2. 安装所需科学包

`conda install -n Materials -c conda-forge ase` 将ase自动安装到材料虚拟环境

### 3. 注意检查安装情况

最新版anaconda自带的py是3.7.4，而ase整合的py是3.8.1

### 4. 使用cmd而不是powershell

VScode如果采用默认终端，是powershell，而这会导致奇怪bug，用cmd就可以完美避开这些坑

## 2. VSCode设置

### 1. 解释器的选择

VSCode左下角可以选择解释器，但这还不够，实际执行的时候还是会在默认base环境中运行，这样无法导入特定虚拟环境中的安装包，会导入错误

### 2. 终端切换虚拟环境

`ctrl+shift+P`搜索`settings.json`，选择`open settings(json)`不是default的那个！

新建一个终端，在右下角的下拉框中可以选择默认shell，第一个就是cmd，选中它后settings.json文件中就会加一行`"terminal.integrated.shell.windows": "C:\\WINDOWS\\System32\\cmd.exe"`

在`settings.json`中添加类似这样一段代码，其中路径根据自己实际情况修改：

```json
"python.pythonPath": "C:\\Users\\DeeliN\\Anaconda3\\envs\\Materials\\python.exe",
"python.autoComplete.extraPaths": [
    "C:\\Users\\DeeliN\\Anaconda3\\envs\\Materials",
    "C:\\Users\\DeeliN\\Anaconda3\\envs\\Materials\\Lib\\site-packages"
    ],
"python.autoComplete.addBrackets": true,
```

删除所有终端，再点击.py文件右上角的播放按钮`run python in terminal`就会自动打开cmd终端，执行`conda activate Materials`切换到指定虚拟环境并开始运行文件显示结果，debug模式同理
