odoo模块开发以及相关技术入门介绍

# odoo开发入门介绍

## 远程环境

* 远程环境

![SSH环境](assets/img_01.png)

* 远程部署

![SFTP部署](assets/img_02.png)

* 远程调试


>  补充：pip内网私服:http://center.tlrfid.tl/repository/pypi-public/simple，可直接将center.tlrfid.tl指向\*.32，也可设置DNS为\*.6，但不能直接直接用IP。

## 项目目录

* addons

* odoo

* odoo.conf

* odoo-bin

  命令行直接加参数好像不支持自定义目录，需要定义odoo.conf。

## 模块构建

```
#source ***venv/odoo/bin/python
#odoo-bin scaffold <module name> <path>
```

如果是远程的话需要从远程同步下来。

## 模块目录

* 基本信息manifest
  * 包括`名称name`，描述description，`作者author`，作者网站地址website，`版本version`，`基础数据data`，演示数据demo，分类category，`依赖depends`，许可license，是否自动安装auto_install，是否为应用application，样式集css，是否可网页安装installable，钩子hook（pre_init_hook前执行、post_init_hook安装后和uninstall_hook卸载后）。

  > 文档：https://www.odoo.com/documentation/10.0/reference/module.html

* 静态资源static
  * 模块介绍及应用图标，除了可以在基本信息中添加以外，我们也可以这里也做详细的图文介绍等。
  * 其他资源，包括相关图片、CSS、JS、Less等。

  > 如：account/static

* 网页控制器Web controllers

  * 地址路由Routing
  * 请求Request
  * 响应Response
  * 常规控制器Controllers

  > 如：web/controllers/main.py

* 常规数据data

  * 基础数据
  * 如：account/data/account_data.xml

* 演示数据

  > 如：account/demo/account_demo.xml

* 文档doc

  * 可以直接生成html

  > 如：web/doc/index.rst

* 语言翻译i18n

  > 如：account/i18n/zh_CN.po

* 映射模型models

  > 如：sale/models/res_partner.py

* 视图views

  * 菜单
  * 动作
  * 视图

  > 如：sale/views/sale_views.xml
  >
  > 注意：顺序不能变，至上而下，否则可能会报错。

* 权限security

  * 分组控制Group
  * 访问权限Access
  * 记录规则Rule

  > 如：sale/security

* 报表report

  > 如：sale/report

* 测试

  > sale/tests/test_product_id_change.py

* wizard向导

  * TransientModel临时模型|瞬态
  * 一定时间自动删除
  * 不需要权限

  > 如：addons/account/wizard/account_invoice_refund_view.xml

* 初始化信息init

  > 如：odoo/__init__.py，purchase/__init__.py

## 文件命名

* 常规命名

  * models/*<main_model>*.py
  * models/*<inherited_main_model>*.py
  * views/*<main_model>*_templates.xml
  * views/*<main_model>*_views.xml

  >  如：sale_order_dates/sale_order.py |sale_order_views.xml
  >
  > account/models/account_journal_dashboard.py
  >
  > 文档：https://www.odoo.com/documentation/10.0/reference/guidelines.html#module-structure

## XML文件

*  一般格式

  ```xml
  <record id="view_id" model="ir.ui.view">
      <field name="name">view.name</field>
      <field name="model">object_name</field>
      <field name="priority" eval="16"/>
      <field name="arch" type="xml">
          <tree>
              <field name="my_field_1"/>
              <field name="my_field_2" string="My Label" widget="statusbar" statusbar_visible="draft,sent,progress,done" />
          </tree>
      </field>
  </record>
  ```

* 精简格式|直接标签

  * menuitem
  * template
  * report
  * kanban

* 继承与扩展

  ```xml
  <record id="inherited_model_view_form_inherit_my_module" model="ir.ui.view">
      ...
  </record>
  ```

## python一般规范

* 尊重PEP8规范

  * E501: line too long
  * E301: expected 1 blank line, found 0
  * E302: expected 2 blank lines, found 1
  * E126: continuation line over-indented for hanging indent
  * E123: closing bracket does not match indentation of opening bracket's line
  * E127: continuation line over-indented for visual indent
  * E128: continuation line under-indented for visual indent
  * E265: block comment should start with '# '
  * 建议尽量适应和统一Code style

* 其他格式

  * 编码头

    ```python
    # -*- coding: utf-8 -*-
    ```

  * 复制与克隆

    ```python
    # bad
    new_dict = my_dict.clone()
    new_list = old_list.clone()
    # good
    new_dict = dict(my_dict)
    new_list = list(old_list)

    ```

  * 字典创建与更新

    ```python
    # -- creation with values
    # bad
    my_dict = {}
    my_dict['foo'] = 3
    my_dict['bar'] = 4
    # good
    my_dict = {'foo': 3, 'bar': 4}

    # -- update dict
    # bad
    my_dict['foo'] = 3
    my_dict['bar'] = 4
    my_dict['baz'] = 5
    # good
    my_dict.update(foo=3, bar=4, baz=5)
    my_dict = dict(my_dict, **my_dict2)
    ```

> 如：https://www.python.org/dev/peps/pep-0008/
>
> https://blog.csdn.net/ratsniper/article/details/78954852

## 源码了解

* 会计模块account_accountant
* 采购模块purchase
* 库存模块stock
* 销售模块sale
* 自定义模块leave

## 开发参考

* [映射模型ORM](module.md)
* [数据文件data](module.md)
* [菜单menu](module.md)
* [动作actions](module.md)
* [视图views](module.md)
* [模块module](module.md)
* [命令行cmdline](module.md)
* [控制器controllers](module.md)
* [工作流workflow](module.md)
* [安全机制security](module.md)
* [报表report](module.md)
* [基本继承inherit](module.md)
* [官方文档documentation](module.md)
* [案例example](module.md)