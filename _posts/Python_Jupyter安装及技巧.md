
### Python_Jupyter安装
安装搭建Python jupyter环境参考网址：
<https://www.cnblogs.com/postgres/p/6926198.html>
<br>  
如何安装并设置Jupyter登录密码：
2. 安装：pip install jupyter
3. 生成jupyter的配置文件：jupyter notebook --generate-config （注:生成的配置文件名为jupyter_notebook_config.py）
3. 控制台继续输入：jupyter notebook password （会输入两次密码，用来验证）
3. 密码设置成功（默认会在Users\\(username)\\.jupyter的目录下生产一个单独jupyter_notebook_config.json的密码文件）。 
3. 测试：1.启动jupyter服务器： jupyter notebook；2.在弹出的web窗口中点击Loginout（右上角）； 3.输入登录密码，成功进入！

jupyter_notebook_config.py配置文件一般也在Users\\(username)\\.jupyter的目录，其基本的配置参数为：
```python
## ------开始基本的参数配置------
## The IP address the notebook server will listen on. default is 'localhost'
c.NotebookApp.ip = '*'           # '*'代表所有iP都能访问,也可以指定ip

## The port the notebook server will listen on.
c.NotebookApp.port = 8888

## The directory to use for notebooks and kernels.
c.NotebookApp.notebook_dir = 'D:\Python\jupyterSrc'

## Whether to open in a browser after starting. The specific browser used is
#  platform dependent and determined by the python standard library `webbrowser`
#  module, unless it is overridden using the --browser (NotebookApp.browser)
#  configuration option.
c.NotebookApp.open_browser = False      # 禁止自动打开浏览器
c.PAMAuthenticator.encoding = 'utf8'    # 指定utf-8编码，解决读取中文路径或者文件乱码问题
## ------结束配置------
```

**启动Notebook服务器(可加启动参数)：**
```
$ jupyter notebook
$ jupyter notebook my_notebook.ipynb   # 打开my_notebook.ipynb
$ jupyter notebook --port 9999   # 设置自定义端口
$ jupyter notebook --no-brower   # 启动时不打开浏览器
$ jupyter notebook --ip="*"      # 允许任意IP连接，可用于局域网共享
$ jupyter notebook --help        # 帮助信息
```

### Python_Jupyter技巧

#### 一、技巧资料文档网址：
Jupyter Notebook的27个秘诀，技巧和快捷键网页链接:  <br>
     https://www.zybuluo.com/hanxiaoyang/note/534296;<br>
(原文)https://www.dataquest.io/blog/jupyter-notebook-tips-tricks-shortcuts/

#### 二、历史代码恢复
在jupyter notebook上使用IPython写了大段代码，却不小心误删，同时由于jupyter notebook只有一个存档位，代码没有存档，或存档过久，因此无法恢复原内容怎么办？ 可以利用IPython强大的交互能力恢复出来！！<br>
不要关闭jupyter notebook, 而是继续执行下面的代码:
```python
for line in locals()['In']:
    print(line)

#或者， 直接执行下面命令
history
```
过往的输入历史就能很方便的显现出来， 然后手动恢复吧

#### 三、代码自动补全
让jupyter notebook实现自动代码补全，首先安装 nbextensions
```
pip install jupyter_contrib_nbextensions
jupyter contrib nbextension install --user```
然后安装 nbextensions_configurator
```
pip install jupyter_nbextensions_configurator```
如果提示缺少依赖，就使用pip安装对应依赖即可。
最后重启jupyter notebook，在弹出的主页面里，能看到增加了一个Nbextensions标签页，在这个页面里，勾选Hinterland即启用了代码自动补全。（有时不能看到Nbextensions标签页,则可能在edit菜单最下面会有nbextensions config菜单项）  

附：参考其它nbextensions插件使用：
[高效方法:Jupyter Notebook比你想象中的还要强大](https://www.songma.com/news/txtlist_i28408v.html)

#### 四、魔术命令(magic commands)

魔术命令（magic commands），正如其名，是用于控制notebook的特殊的命令。它们运行在代码单元中，以 % 或者 %% 开头，前者控制一行，后者控制整个单元。

比如，使用 %run 命令运行脚本；要得到代码运行的时间，则可以使用 %timeit；如果要在文档中显示 matplotlib 包生成的图形，则使用 % matplotlib inline；如果要做代码调试，则使用 %pdb。但注意这些命令大多是在Python kernel 中适用的，其他 kernel 大多不适用。有许许多多的魔术命令可以使用，详细的命令清单请参考 [Built-in magic commands](https://ipython.readthedocs.io/en/stable/interactive/magics.html)。

#### 五、运行系统Command命令
jupyter的cell可以作为unix(或者windows) 命令行命令使用，
具体方法为：在command前面加入一个感叹号“！”，如：
````
!dir           # windows命令
!ls -ls        # Linux命令
```

#### 六、导入py代码
将本地的.py文件load到jupyter的一个cell中。py文件需在jupyter工作目录的相对文件夹下，见下示例：  
运行下述cell代码，就会将load后面所对应地址的代码load到当前的cell中。运行后%load后，该代码自动加入了注释符号#  
```
%load pandas_test/pandas_tolist.py```
也可以从网络http地址上load代码到jupyter，如下：  
```
%load http://。。。/test.py```

#### 七、安装支持其它语言
Jupyter Notebook可以支持的编程语言列表详细参考如下网址：  
https://github.com/jupyter/jupyter/wiki/Jupyter-kernels

[julia简易教程——安装Julia+jupyter notebooks](https://blog.csdn.net/wcy23580/article/details/82843292)

[在jupyter notebook中使用R语言](https://blog.csdn.net/ICERON/article/details/82743930)

#### 九、如何用一台服务器给多个Jupyter用户提供服务
&emsp;&emsp;团队有多个人想在master上用jupyter操作，又不方便大家用一个账户，于是就创建了多个账户。
方法很简单：  
jupyter notebook 命令有一个 --config <config_file_path> 的可选参数，默认使用当前目录下的jupyter_notebook_config.py配置文件，可填入其它配置文件的绝对路径 以启用对应配置。

只要给每个用户写一个配置文件（至少端口、工作目录的配置要不同），然后分别运行下行命令即可。  
>jupyter notebook --config jupyter_notebook_config_username.py
具体如下示例（执行下行命令启动服务）：  
>jupyter note book --config /root/.jupyter/jupyter_note_book_config_hs.py  

注：jupyter_note_book_config_hs.py配置文件中，至少password、port与notebook_dir参数，应与默认jupyter_notebook_config.py配置文件的不同。
这样，客户端在浏览器上 通过 <ip地址>:7777 访问。  
至此，该服务器就可以给多个端口、密码不同的 jupyter notebook 用户使用了。详细使用参考网址见下：  
https://blog.csdn.net/jjwho/article/details/75102045

### 后记：Jupyter Notebook介绍
&emsp;&emsp;在介绍 Jupyter Notebook 之前，让我们先来看一个概念：**文学编程** (Literate programming)。简单来说，文学编程的读者不是机器，而是人。我们从写出让机器读懂的代码，过渡到向人们解说如何让机器实现我们的想法，其中除了代码，更多的是叙述性的文字、图表等内容。这么一看，这不正是数据分析人员所需要的编码风格么？不仅要当好一个程序员，还得当好一个作家。那么Jupyter Notebook就是不可或缺的一款集编程和写作于一体的效率工具。

&emsp;&emsp;其实Jupyter 脱胎于大名鼎鼎的**IPython**项目，IPython顾名思义，是专注于Python的项目，但随着项目发展壮大，已经不仅仅局限于Python这一种编程语言了，除Python之外的其他语言（Julia、Haskell、R等）的内核就被连续地创建了出来。Jupyter的名字就很好地释义了这一发展过程，它是Julia、Python以及 R 语言(数据科学的三种开源语言)的组合，字形相近于木星（Jupiter），但这个名字代表了超越了任何特定语言的通用思想：即计算、数据和人类的理解、共享和协作的活动。

&emsp;&emsp;Jupyter Notebook使用浏览器作为界面，向后台的IPython服务器发送请求，并显示结果。在浏览器的界面中使用单元(Cell)保存各种信息。Jupyter Notebook 的本质是一个Web应用程序，便于创建和共享文学化程序文档，支持实时代码，数学方程，可视化和markdown。

**Jupyter Notebook 的众多优点：**

+ 极其适合数据分析<br>
想象一下如下混乱的场景：你在终端中运行程序，可视化结果却显示在另一个窗口中，包含函数和类的脚本存在其他文档中，更可恶的是你还需另外写一份说明文档来解释程序如何执行以及结果如何。此时 Jupyter Notebook 从天而降，将所有内容收归一处，你是不是顿觉灵台清明，思路更加清晰了呢？

+ 支持多语言<br>
也许你习惯使用 R 语言来做数据分析，或者是想用学术界常用的 MATLAB 和 Mathematica，这些都不成问题，只要安装相对应的核（kernel）即可。这里列出了 Jupyter 支持的所有语言，供您参考。

+ 分享便捷<br>
支持以网页的形式分享，GitHub 中天然支持 Notebook 展示，也可以通过 nbviewer 分享你的文档。当然也支持导出成 HTML、Markdown 、PDF 等多种格式的文档。

+ 远程运行<br>
在任何地点都可以通过网络链接远程服务器来实现运算，这里给出一个远程运行的例子，可以体验一下 Jupyter Notebook。

+ 交互式展现<br>
不仅可以输出图片、视频、数学公式，甚至可以呈现一些互动的可视化内容，比如可以缩放的地图或者是可以旋转的三维模型。这就需要交互式插件（Interactive widgets）来支持，更多内容请参考这里。

**内核**

Jupyter Notebook与IPython终端共享同一个内核。内核进程可以同时连接到多个前端。在这种情况下，不同的前端访问的是同一个变量。  
这个设计可以满足以下两种需求:
```
相同内核不同前端，用以支持，快速开发新的前端
相同前端不同内核，用以支持，新的开发语言```
