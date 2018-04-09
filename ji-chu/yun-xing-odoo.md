## 1. 下载源代码

odoo源代码托管在github上，包括了从5开始的各个版本，目前最新版本是odoo11，但是据测试odoo11还不太稳定，但是开始尝试性地支持`ppython3` 了，可以预见odoo支持`python3` 应该也不远了，odoo12应该在2018年10月份左右发布，本书使用odoo的稳定版10。同时 [https://nightly.odoo.com](https://nightly.odoo.com) 也提供构建，但是我测试时遇到问题，推荐使用[https://github.com/odoo/odoo](https://github.com/odoo/odoo)下载源代码进行构建。也可以使用git获取完全源代码`$ git clone https://github.com/odoo/odoo.git`

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

odoo依赖很多，在源代码中有一个文件`requirements.txt`  可以使用 `$ pip install -r requirements.txt`  命令进行安装，遗憾的是有的包需要编译和不支持pip安装，所以需要特殊处理，经过测试，以下包需要单独下载安装：

> python-ldap，pwin32 wkhtml2pdf

需要编译的包在windows下比较困难，好在 [https://www.lfd.uci.edu/~gohlke/pythonlibs/](https://www.lfd.uci.edu/~gohlke/pythonlibs/) 网上有很多编译好的包，安装失败的包可以下载后使用 `$ pip install *.whl` 进行安装。

还有一个包是将html转为pdf的工具 `wkhtmltox`，需要单独安装，其次是windows下需要安装 pywin32 ,pywin32可以直接到 [https://sourceforge.net/projects/pywin32/](https://sourceforge.net/projects/pywin32/) 网上下载响应版本进行安装，选择32位64位不是依据操作系统，而是python解释器的版本，不过最近pywin32也支持pip 安装，但是需要修改  `requirements.txt`文件，`pypiwin32 ; sys_platform == 'win32'`

之后修改 `requirements.txt`文件，将手动安装的包注释，在执行`$ pip install -r requirements.txt`

命令完成安装。

## 3.nodejs依赖

下载nodejs安装

安装less`$ npm install -g less`

## 4. 运行odoo服务

` python odoo-bin -w odoo -r odoo --addons-path=addons,../mymodules --db-filter=mydb$`

使用浏览器进行访问，默认端口为8069

# linux下安装odoo10

> linux系统下安装,以debian为例
>
> debian默然安装python2.7,
>
> 安装pip工具
>
> 安装virtualenv

1. 创建odoo用户
  ```bash
  sudo adduser odoo
  ```

2. 刷新系统
  ```bash
  sudo apt update && sudo apt upgrade -y
  ```

3. 安装系统依赖

    ```bash
    sudo apt-get install libxml2-dev libxslt-dev python-dev libldap2-dev libsasl2-dev
    ```

4. 安装nodeJs,less

    ```bash
    sudo apt-get install -y npm
    sudo ln -s /usr/bin/nodejs /usr/bin/node
    sudo npm install -g less
    ```

5. 安装依赖包
    ```bash
    sudo apt-get install -y python3-pip
    sudo pip3 install Babel decorator docutils ebaysdk feedparser gevent greenlet html2text Jinja2 lxml Mako MarkupSafe mock num2words ofxparse passlib Pillow psutil psycogreen psycopg2 pydot pyparsing PyPDF2 pyserial python-dateutil python-openid pytz pyusb PyYAML qrcode reportlab requests six suds-jurko vatnumber vobject Werkzeug XlsxWriter xlwt xlrd
    ```

6. 安装数据库

    ```bash
    sudo apt-get install -y postgresql
    ```

7. 给数据库建个odoo账号让odoo源码运行的时候有权限对数据库进行读写操作

    ```bash
    sudo su - postgres
    createuser --createdb --username postgres --no-createrole --no-superuser --pwprompt odoo
    ```

8. 获取odoo10源码

    ```bash
    git clone https://www.github.com/odoo/odoo --branch 10.0 --depth 1 --single-branch ./odoo10
    ```

9. 源码运行odoo10生成一个配置文件

    ```bash
    cd ~/odoo10
    ./odoo-bin -s
    ```

10. 设置配置文件

    ```bash
    sudo mkdir /etc/odoo
    sudo cp /home/odoo/.odoorc /etc/odoo/odoo.conf
    sudo chown -R odoo /etc/odoo
    ```

    ​

11. 设置odoo日志

     ```bash
     sudo mkdir /var/log/odoo
     sudo chown odoo /var/log/odoo
     ```

     ​

12. 修改odoo配置

     `sudo vi /etc/odoo/odoo.conf`

     ```ini
     [options]
     logfile = /var/log/odoo/odoo.log
     logrotate = True
     ```

     ​

13. 安装中文字体

     ```bash
     sudo apt-get install ttf-wqy-zenhei -y
     sudo apt-get install ttf-wqy-microhei -y
     ```

     ​

14. 安装报表所需wkhtmltopdf

     ```bash
     wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.2.1/wkhtmltox-0.12.2.1_linux-trusty-amd64.deb
     ```

     ```bash
     sudo dpkg -i wkhtmltox-0.12.2.1_linux-trusty-amd64.deb
     sudo ln -s /usr/local/bin/wkhtmltopdf /usr/bin
     sudo ln -s /usr/local/bin/wkhtmltoimage /usr/bin
     ```

     ​

15. 让odoo随系统自动启动

     `sudo vi /lib/systemd/system/odoo.service`

     内容如下：

     ```ini
     [Unit]
     Description=Odoo
     After=postgresql.service
     [Service]
     Type=simple
     User=odoo
     Group=odoo
     ExecStart=/home/odoo/odoo10/odoo-bin -c /etc/odoo/odoo.conf
     [Install]
     WantedBy=multi-user.target
     ```

     ​

16. 注册为系统服务

     ```bash
     sudo systemctl enable odoo.service
     ```

     ​

17. 启动服务

     ```bash
     sudo systemctl start odoo
     ```

     ​

