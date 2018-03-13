## 1. 下载源代码

odoo源代码托管在github上，包括了从5开始的各个版本，目前最新版本是odoo11，但是据测试odoo11还不太稳定，但是开始尝试性地支持`ppython3` 了，可以预见odoo支持`python3` 应该也不远了，odoo12应该在2018年10月份左右发布，本书使用odoo的稳定版10。同时 [https://nightly.odoo.com](https://nightly.odoo.com) 也提供构建，但是我测试时遇到问题，推荐使用[https://www.gitbook.com/book/bestchu/odoo10](https://www.gitbook.com/book/bestchu/odoo10)下载源代码进行构建。

## 2. python环境

odoo10只支持python2，我们先安装python2，到[https://www.python.org/](https://www.python.org/)上下载pythin2的最新版本，如果安装有其它版本的python，选择不添加path环境。

一般安装好python后自动安装python的pip包管理工具，如果没有请到[https://pip.pypa.io/en/stable/](https://pip.pypa.io/en/stable/)网下载[get-pip.py](https://bootstrap.pypa.io/get-pip.py) 使用一下命令进行安装：

```
$ python get-pip.py
```

> 注意系统中有多个版本的python是一定要设置path环境变量，set path=D:\python\Python27；D:\python\Python27\Scripts；%path%在执行。

为了避免包冲突，一般推荐使用虚拟环境，虚拟环境使用如下命令安装

```
$ pip install virtualenv
```

创建虚拟按环境：

```
virtualenv --no-site-packages venv -p D:\python\Python27\python.exe
```

激活虚拟按环境：

```
$ source venv/bin/activate
```

windows下使用：

```
ven/Script/activate.bat
```

之后就可以使用pip进行安装依赖。

# 2.安装依赖

odoo依赖很多，在源代码中有一个文件`requirements.txt`  可以使用 `$ pip install -r requirements.txt`  命令进行安装，遗憾的是有的包需要编译和不支持pip安装，所有需要特殊处理，经过测试，一下包需要单独下载安装：

> python-ldap

需要编译的包在windows下比较困难，好在 [https://www.lfd.uci.edu/~gohlke/pythonlibs/](https://www.lfd.uci.edu/~gohlke/pythonlibs/) 网上有很多编译好的包，安装失败的包可以下载后使用 `$ pip install *.whl` 进行安装。

还有一个包是将html转为pdf的工具 `wkhtmltox`，需要单独安装，其次是windows下需要安装 pywin32 ,pywin32可以直接到 [https://sourceforge.net/projects/pywin32/](https://sourceforge.net/projects/pywin32/) 网上下载响应版本进行安装，选择32位64位不是依据操作系统，而是python解释器的版本，不过最近pywin32也支持pip 安装，但是需要修改  `requirements.txt`文件，`pypiwin32 ; sys_platform == 'win32'`

之后修改 `requirements.txt`文件，将手动安装的包注释，在执行`$ pip install -r requirements.txt`

命令完成安装。

## 3. 运行odoo服务

使用odoo-bin进行运行

–xmlrpc-port=8888

–addons-path=addons

–db\_user

–database

–db\_password

