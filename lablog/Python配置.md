# Python配置

>环境变量中的用户变量与系统变量的区别：https://zhuanlan.zhihu.com/p/93719752
>
>1. 环境变量没有区分大小写，例如path跟PATH是一样的。
>2. 系统变量对所有用户有效；用户变量只对当前用户有效。
>3. 用户变量与系统变量，名称是变量，值是里面的内容，也就是通过变量存储了想要存储的内容，方便调用。
>4. 系统变量与用户变量的PATH：告诉系统可执行文件放在什么路径（平常执行程序的路径，要放在PATH里面，不能建一个变量，cmd会提示“不是内部或外部命令，或者不是可执行程序”）。
>5. windows系统在执行用户命令时，若用户未给出文件的绝对路径，则首先在当前目录下寻找相应的可执行文件、批处理文件等。
>6. 若果当前目录找不到对应文件名的程序，在系统变量的PATH的路径中，依次寻找对应的可执行程序文件（查找顺序是按照路径的录入顺序从左往右寻找的，最前面一条的优先级最高，如果找到程序就停止寻找，后面的路径不再执行）
>7. 如果系统变量的PATH的路径找不到，再到用户变量的PATH路径中寻找（如果系统变量和用户变量的PATH中同时包含了同一个命令，则优先执行系统变量PATH中的命令）
>8. 每次新加了命令以后，要确定保存了。再重启CMD，否则命令不生效的。
>9. 在CMD里要输出环境变量 ECHO %变量名%



# 1 Miniconda

Miniconda=conda+python+一些基本包

## 1.1 Miniconda安装及添加环境变量

https://mp.weixin.qq.com/s/yqyEknvYLIH5E0nMlWEDSQ

添加环境变量：

“系统”——“高级系统设置”——“环境变量”——单击”用户变量“中的“Path”，选择“编辑”进入：

“新建”三个路径（Miniconda安装路径为R:\Miniconda），==为了防止cmd里输入python弹出WindowsAPP应用商店的界面，把这些用户变量加在最前面==：

```
R:\Miniconda
R:\Miniconda\Scripts
R:\Miniconda\Library\bin
```

> 不用配置环境变量在cmd命令行里执行命令，还可以在Anaconda Prompt里执行命令，一样的。

本机python版本：3.9.12

## 1.2 基本操作

https://www.shuzhiduo.com/A/D854QkP3dE/

列出当前环境的所有软件包

```python
conda list
```

更新包，跟安装一样的命令，会自动更新。

### 虚拟环境

查看创建的环境

```python
conda info --envs/e
```

> 默认会有个原始的base环境。

创建环境

```python
#创建一个名叫ml，使用python3.9解释器的虚拟环境 -n是虚拟环境名字，python = 3.9是指定特定版本，若不指定，则安装原有miniconda版本的python解释器
conda create -n ml python=3.9
#克隆一个虚拟环境
conda create --name <yourEnv> --clone <baseEnv>

#激活环境
conda activate ml
#停用环境
conda deactivate
```

每次打开终端都会激活其默认的base环境，我们可通过以下命令，禁止激活默认base环境

```python
conda config --set auto_activate_base false
```

虚拟环境的文件在```R:\Miniconda\envs```下查看，安装的包在```R:\Miniconda\envs\ml\Scripts```中查看。

删除虚拟环境

```python
# 第一步：首先退出环境
conda deactivate
 
# 第二步：删除环境
conda remove -n  需要删除的环境名 --all
```

### 换源

显示所有conda的channel ：

```bash
conda config --show channels
```

```python
# 清华的镜像源
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
# 中国科技大学源
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/msys2/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/bioconda/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/menpo/
# 阿里云的服务器
http://mirrors.aliyun.com/pypi/simple/
# 豆瓣网站是用python做的呀 豆瓣的python的源
conda config --add channels http://pypi.douban.com/simple/
```

```python
# 设置搜索时显示通道地址
conda config --set show_channel_urls yes
```

删除镜像源

```
conda config --remove channels http://mirrors.aliyun.com/pypi/simple/
```

### 安装、删除包

conda 安装命令：

```bash
conda install XXX
```

卸载命令：

```bash
conda uninstall XXX
```

这个命令时不时会出一些问题，卸载失败。这个时候，就可以尝试以下两种卸载命令：

```bash
conda remove XXX
pip uninstall  XXX
```

注意：
安装的时候是用pip 安装， 卸载的时候也需要pip uninstall

### 常见问题

#### Sublime Text 4的使用

如果电脑中安装的是非官方的python环境（如miniconda anaconda），采用Sublime Text 4运行python文件时会报错```[WinError 2] 系统找不到指定的文件```，问题来源于Sublime Text更新了调用 Python的命令行指令：旧版本中调用的命令为`python`，而在新版中改为了`py`，但是问题在于，前面说的那些第三方 Python 环境砍掉了这个功能，conda 的环境中根本没有`py.exe`这个文件，就导致了`py`命令无法被识别而报错。

解决方案：在Python的安装目录下，找到`python.exe`，复制到另一个地方，改名为`py.exe`，再拖回Python的安装目录。

在Sublime Text 4里使用虚拟环境：

Sublime Text 4的“Tools”——“Build System”——“New Build System”，在`sublime-build`文件中覆盖以下代码：

```json
{
    "shell":true,
    "cmd": ["R:\\Miniconda\\envs\\ml\\python.exe", "$file"],
    "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
    "selector": "source.python"
}
```

“cmd”字段里设置目标虚拟环境中的python解释器python.exe的路径，保存到默认地址，命名为`Python(ml).sublime-build`，可以自由命名，后缀一定要是`sublime-build`。

# 2 安装包

## Jupyter Notebook

Anaconda Prompt中输入

```
conda install jupyter notebook
```

如果你不想在Jupyter Notebook中编写的所有文档都直接保存启动目录下，则需要修改Jupyter Notebook的文件存放路径。可以按照如下步骤完成：

输入

```
jupyter notebook --generate-config
```

出现

```
Writing default config to: C:\Users\12576\.jupyter\jupyter_notebook_config.py
```

接着就找到C:\Users\12576\.jupyter\jupyter_notebook_config.py文件，并修改内容：

```python
c.NotebookApp.notebook_dir = ''
```

为

```python
c.NotebookApp.notebook_dir = 'R:\JupyterNotebook_file' #记得前面空格删干净
```

测试，输入

```
jupyter notebook
```

查看路径是否修改成功。

Jupyter Notebook的执行文件是```R:\Miniconda\envs\ml\Scripts\jupyter-notebook.exe```，可以右键将其固定到开始屏幕，打开更为方便。

在新环境ml下安装的包，如果import出错```DLL load failed while importing ......: 找不到指定模块```，应该是环境变量没添加，在环境变量的“Path”中“新建”```R:\Miniconda\envs\ml\Library\bin```，即可。

> 软件包一旦有增删，一定要重新启动jupyter notebook，才能生效。

## 其他

```
conda install numpy
conda install scikit-learn
conda install selenium
conda install pandas
conda install matplotlib
conda install seaborn
```
