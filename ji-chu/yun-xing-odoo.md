## 1. 下载源代码

odoo源代码托管在github上，包括了从5开始的各个版本，目前最新版本是odoo11，但是据测试odoo11还不太稳定，但是开始尝试性地支持`ppython3` 了，可以预见odoo支持`python3` 应该也不远了，odoo12应该在2018年10月份左右发布，本书使用odoo的稳定版10。同时 [https://nightly.odoo.com](https://nightly.odoo.com) 也提供构建，但是我测试时遇到问题，推荐使用[https://www.gitbook.com/book/bestchu/odoo10](https://www.gitbook.com/book/bestchu/odoo10)下载源代码进行构建。

## 2. python环境

odoo10只支持python2，我们先安装python2，到[https://www.python.org/](https://www.python.org/)上下载pythin2的最新版本，如果安装有其它版本的python，选择不添加path环境。

一般安装好python后自动安装python的pip包管理工具，如果没有请到[https://pip.pypa.io/en/stable/](https://pip.pypa.io/en/stable/)网下载[get-pip.py](https://bootstrap.pypa.io/get-pip.py) 使用一下命令进行安装：

```
$ python get-pip.py
```

> 注意系统中有多个版本的python是一定要选择好path环境，set path=

安装虚拟环境，安装python是一般都会安装pip包管理工具，如果没有pip管理工具请继续往下看，使用 ```pip install ``

# 2.安装依赖

源代码中有一个文件\`[requirements.txt](https://github.com/odoo/odoo/blob/11.0/requirements.txt)``可以使用`pip install -r``[requirements.tx](https://github.com/odoo/odoo/blob/11.0/requirements.txt)\`

