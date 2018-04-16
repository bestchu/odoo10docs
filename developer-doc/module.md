开发主要参考odoo官网

# 开发参考

## 映射模型ORM

* 通用属性，string标签名称，required是否必须|是否可为空，help提示语，index是否索引等

* 基本类型，Boolean，Date，Char，Integer等

* 方法字段Creating Models

* 计算字段|依赖字段，依赖于其他字段，需要@api.depends装饰符

* 关联字段

  ```python
  nickname = fields.Char(related='user_id.partner_id.name', store=True)
  ```

* 模型关联，Many2one，One2many以及Many2many

* 保留字段，比如id，create_date，write_uid等

![fields.py](assets/img_05.png)

> 文档：https://www.odoo.com/documentation/10.0/reference/orm.html#environment

## 数据文件data

* 文件结构Structure
* 记录record
* 视图
* 动作
* 菜单
* 权限
* 模板

> 文档：https://www.odoo.com/documentation/10.0/reference/data.html

## 菜单menu

* ir.ui.menu=menuitem
* 源码了解

> 文档：https://www.odoo.com/documentation/10.0/reference/data.html#shortcuts

## 动作actions

* 窗体ir.actions.act_window
* 链接ir.actions.act_url
* 报表ir.actions.report.xml
* 服务器ir.actions.server
* 客户端ir.actions.client
* 触发方式，菜单项，按钮以及上下文动作等
* 源码了解

> 文档：https://www.odoo.com/documentation/10.0/reference/actions.html

## 视图views

* 常规结构与属性

  * name
  * model
  * arch
  * groups_id
  * inherit_id

* 继承Inheritance

  * model
  * arch

* 列表参数Tree

  * `default_order`

  * `decoration-{$name}`

  * `create`, `edit`, `delete`

  * `button`

  * `field`

    > 文档：https://www.odoo.com/documentation/10.0/reference/views.html#common-structure
    >
    > 注意：有的已经销毁过时

* 视图类型

  * tree列表视图

  * form表单视图

    * 结构组件Structural components
    * 重要组件Semantic components
    * 业务视图布局Business Views guidelines
    * 弹窗Dialog
    * 样式

    > 文档：https://www.odoo.com/documentation/10.0/reference/views.html#forms

  * search搜索视图

    * 字段field

    * 过滤filter

      ```xml
      <record id="leave.search_view" model="ir.ui.view">
                  <field name="model">leave.leave</field>
                  <field name="arch" type="xml">
                      <search string="leave">
                          <filter string="draft" name="services" domain="[('state','=','draft')]"/>
                          <filter string="done" name="services" domain="[('state','=','done')]"/>
                          <separator/>
                      </search>
                  </field>
              </record>
      ```

      ​

    > 文档：https://www.odoo.com/documentation/10.0/reference/views.html#search

  * kanban看板视图

    * 模板templates

    * 字段field

      ```xml
      <record id="leave.kanban_view" model="ir.ui.view">
                  <field name="model">leave.leave</field>
                  <field name="arch" type="xml">
                      <kanban class="leave_kanban">
                          <field name="title"/>
                          <field name="person"/>
                          <field name="state"/>
                          <field name="start_date"/>
                          <templates>
                              <t t-name="kanban-box">
                                  <div class="oe_kanban_card">
                                      <a type="open">
                                          <t>person</t>
                                          <field name="person"/>
                                          <t>
                                              <br/>
                                          </t>
                                          <t>days</t>
                                          <field name="days"/>
                                          <t>
                                              <br/>
                                          </t>
                                          <t>start_date</t>
                                          <field name="start_date"/>
                                          <t>
                                              <br/>
                                          </t>
                                          <t>state</t>
                                          <field name="state"/>
                                          <t>
                                              <br/>
                                          </t>
                                      </a>
                                  </div>
                              </t>
                          </templates>
                      </kanban>
                  </field>
              </record>
      ```

      ​

    > 文档：https://www.odoo.com/documentation/10.0/reference/views.html#kanban

  * graph图表视图

  * gantt视图

  * calendar日历视图

  * pivot透视图

* 显示位置

* 视图源码

> 文档：https://www.odoo.com/documentation/10.0/reference/views.html

## 模块module基本信息

* 前面已经详细介绍

> 文档：https://www.odoo.com/documentation/10.0/reference/module.html

## 命令行cmdline

* 服务启动
  * `--db_host <hostname>`
  * `--db_port <port>`
  * `-r <user>, --db_user <user>`
  * `-w <password>, --db_password <password>`
  * `--xmlrpc-port <port>`
  * `--addons-path=/*/addons/`
* 创建模块
  * 激活环境source等并定位到项目根目录
  * `odoo-bin scaffold <module name> <path>`
* 配置文件
  * 文件位置`*$HOME*/.odoorc`或者自定义`odoo.conf`，当然后面的是通过`--config`或者`-c`参数来设置的，同时前者也会被覆盖，另外还可以通过`--save`来保存当前配置。
  * 大部命令都可以通过配置文件来设置，注意一点，有的参数与命令下的参数不太一样，需要将`-`换成`_`才能被识别。如：--addons-path要换成addons_path

> 文档：https://www.odoo.com/documentation/10.0/reference/cmdline.html#scaffolding

## 控制器controllers

* 地址路由Routing
* 请求Request
* 响应Response
* 常规控制器Controllers

> 如：addons/web/controller/pivot.py
>
> 文档：https://www.odoo.com/documentation/10.0/reference/module.html

## 工作流workflow

* 创建与定义workflow
* 工作流活动模型workflow_activity
* 工作流流转模型workflow_transition

> 文档：https://www.odoo.com/documentation/10.0/reference/workflows.html

## 安全机制security

* 级别
  * menu级访问
  * object级访问
* 分组控制res.groups
* 访问权限ir.model.access
* 记录规则ir.rule

> 文档：https://www.odoo.com/documentation/10.0/reference/security.html

## 报表report

* 模板引擎Qweb，XML生成HTML
* 报表类型report_type，主要有qweb-pdf和qweb-html
* 相关属性，id，name，model等

> 文档：https://www.odoo.com/documentation/10.0/reference/reports.html

## 基本继承inherit

* 模型继承

  ```python
  class BlogPost(models.Model):
      _name = "blog.post"
      _description = "Blog Post"
      _inherit = ['website.published.mixin']
  ```

  ​

* 视图继承

  ```xml
  <record id="inherited_model_view_form_inherit_my_module" model="ir.ui.view">
      ...
  </record>
  ```

  ​

* 模板继承

  ```xml
  <template id="assets_backend" name="account assets" inherit_id="web.assets_backend">
  ...
  </template>
  ```


> 如：addons/account/account_analytic_view.xml
>
> 如：addons/account/account.xml

## 官方文档documentation

* 广泛看资料再看官方文档

> 文档：https://www.odoo.com/documentation/10.0/index.html

## 案例example

* 创建模块

  ```
  #odoo-bin scaffold leave xaddons
  ```

* 编辑模块信息

  ```python
  # -*- coding: utf-8 -*-
  {
      'name': "leave",

      'summary': """
          demo,developing,test""",

      'description': """
          This is my first app for Odoo
      """,

      'author': "showdom",
      'website': "http://www.tlrfid.cn",

      # Categories can be used to filter modules in modules listing
      # Check https://github.com/odoo/odoo/blob/master/odoo/addons/base/module/module_data.xml
      # for the full list
      'category': 'Uncategorized',
      'version': '0.1',

      # any module necessary for this one to work correctly
      'depends': ['base'],

      # always loaded
      'data': [
          # 'security/ir.model.access.csv',
          'views/views.xml',
          'views/templates.xml',
          'views/workflow.xml',
      ],
      # only loaded in demonstration mode
      'demo': [
          'demo/demo.xml',
      ],
      'css': ['static/src/css/leave.css'],
      'installable': True,
      'application': True,
      'auto_install': False,
  }
  ```

* 编辑初始包信息

  ```python
  from . import controllers
  from . import models
  ```

* 编辑详细信息

  * 图标
  * 页面

* 编辑控制器

  ```python
  class Leave(http.Controller):
      @http.route('/leave/leave/', auth='public')
      def index(self, **kw):
          return "Hello, world"
  ```

* 编辑映射模型

  ```python
    # -*- coding: utf-8 -*-

    from odoo import models, fields, api


    class Leave(models.Model):
        _name = 'leave.leave'
        title = fields.Char(string='title', required=True)
        person = fields.Char(string='person', required=True)
        days = fields.Integer(string='days', default=1)
        start_date = fields.Date(string='start date')
        description = fields.Text(string='description')
        money = fields.Float(string='money', compute="_money", store=False)

        @api.depends('days')
        def _money(self):
            self.money = float(self.days) * 100
      
        WORKFLOW_STATE_SELECTION = [
            ('draft', 'Draft'),
            ('confirm', 'Confirm'),
            ('done', 'Done'),
        ]
        state = fields.Selection(WORKFLOW_STATE_SELECTION, default='draft', string="state", readonly=True)
      
        @api.multi
        def action_confirm(self):
            self.state = 'confirm'
            return True
      
        @api.multi
        def action_done(self):
            self.state = 'done'
            return True
  ```

* 编辑基础数据

* 编辑演示数据

  ```xml
  <odoo>
      <data>

          <record id="leave0" model="leave.leave">
              <field name="title">leave0</field>
              <field name="person">liu</field>
              <field name="state">draft</field>
              <field name="days">1</field>
          </record>

          <record id="leave1" model="leave.leave">
              <field name="title">leave1</field>
              <field name="person">zhang</field>
              <field name="state">draft</field>
              <field name="days">2</field>
          </record>
          
          <record id="leave2" model="leave.leave">
              <field name="title">leave2</field>
              <field name="person">zhao</field>
              <field name="state">done</field>
              <field name="days">5</field>
          </record>
      </data>
  </odoo>
  ```

* 编辑视图

  * 编辑Form视图

  ```xml
  <record model="ir.ui.view" id="leave.form_view">
              <field name="name">leave form</field>
              <field name="model">leave.leave</field>
              <field name="arch" type="xml">
                  <form>
                      <header>
                          <button name="confirm" type="workflow" string="confirm" states="draft"
                                  class="oe_highlight" groups="base.group_user"/>
                          <button name="done" type="workflow" string="done" states="confirm"
                                  class="oe_highlight" groups="base.group_user"/>
                          <field name="state" widget="statusbar" statusbar_visible="draft,confirm,done"/>
                      </header>
                      <sheet>
                          <group>
                              <field name="title"/>
                              <field name="person"/>
                              <field name="state"/>
                              <field name="start_date"/>
                          </group>
                      </sheet>
                  </form>
              </field>
          </record>
  ```

  * 编辑Tree视图

  ```xml
  <record model="ir.ui.view" id="leave.tree_view">
              <field name="name">leave list</field>
              <field name="model">leave.leave</field>
              <field name="arch" type="xml">
                  <tree>
                      <field name="title"/>
                      <field name="person"/>
                      <field name="state"/>
                      <field name="start_date"/>
                  </tree>
              </field>
          </record>
  ```


  * `编辑Kanban视图`

  ```xml
  <record id="leave.kanban_view" model="ir.ui.view">
              <field name="model">leave.leave</field>
              <field name="arch" type="xml">
                  <kanban class="leave_kanban">
                      <field name="title"/>
                      <field name="person"/>
                      <field name="state"/>
                      <field name="start_date"/>
                      <templates>
                          <t t-name="kanban-box">
                              <div class="oe_kanban_card">
                                  <a type="open">
                                      <t>person</t>
                                      <field name="person"/>
                                      <t>
                                          <br/>
                                      </t>
                                      <t>days</t>
                                      <field name="days"/>
                                      <t>
                                          <br/>
                                      </t>
                                      <t>start_date</t>
                                      <field name="start_date"/>
                                      <t>
                                          <br/>
                                      </t>
                                      <t>state</t>
                                      <field name="state"/>
                                      <t>
                                          <br/>
                                      </t>
                                  </a>
                              </div>
                          </t>
                      </templates>
                  </kanban>
              </field>
          </record>
  ```

  ​

  * `编辑Search视图`

  ```xml
   <record id="leave.search_view" model="ir.ui.view">
              <field name="model">leave.leave</field>
              <field name="arch" type="xml">
                  <search string="leave">
                      <filter string="draft" name="services" domain="[('state','=','draft')]"/>
                      <filter string="done" name="services" domain="[('state','=','done')]"/>
                      <separator/>
                  </search>
              </field>
          </record>
  ```

  ​

* 编辑动作

  ```xml
  <record model="ir.actions.act_window" id="leave.action_window">
              <field name="name">leave list</field>
              <field name="res_model">leave.leave</field>
              <field name="view_mode">tree,kanban,form</field>
              <field name="help" type="html">
                  <p class="oe_view_nocontent_create">
                      Click to define a new leave.
                  </p>
                  <p>
                      You must define a leave for all,thank you.
                  </p>
                  <p>
                      The leave form contains detailed information to improve the
                      leave process: person,days,start date, etc.
                  </p>
              </field>
          </record>

  ```

* 编辑菜单

  ```xml
  <!-- Top menu item -->
          <menuitem name="leave" id="leave.menu_root"/>
          <!-- menu categories -->
          <menuitem name="Leaves" id="leave.leaves" parent="leave.menu_root"/>
          <!-- actions -->
          <menuitem name="List" id="leave.leaves_tree_view" parent="leave.leaves" action="leave.action_window"/>
  ```

* 编辑工作流

  ```xml
  <odoo>
      <data>
          <!--workflow-->
          <record id="flow_leave_leave" model="workflow">
              <field name="name">workflow</field>
              <field name="osv">leave.leave</field>
              <field name="on_create">True</field>
          </record>
          <!--workflow.activity-->
          <record id="activity_draft" model="workflow.activity">
              <field name="name">draft</field>
              <field name="wkf_id" ref="flow_leave_leave"/>
              <field name="kind">dummy</field>
              <field name="flow_start">True</field>
          </record>
          <record id="activity_confirm" model="workflow.activity">
              <field name="name">confirm</field>
              <field name="wkf_id" ref="flow_leave_leave"/>
              <field name="kind">function</field>
              <field name="action">action_confirm()</field>
          </record>
          <record id="activity_done" model="workflow.activity">
              <field name="name">done</field>
              <field name="wkf_id" ref="flow_leave_leave"/>
              <field name="kind">function</field>
              <field name="action">action_done()</field>
          </record>
          <!--workflow.transition-->
          <record id="transition_draft2confirm" model="workflow.transition">
              <field name="act_from" ref="activity_draft"/>
              <field name="act_to" ref="activity_confirm"/>
              <field name="signal">confirm</field>
          </record>
          <record id="transition_confirm2done" model="workflow.transition">
              <field name="act_from" ref="activity_confirm"/>
              <field name="act_to" ref="activity_done"/>
              <field name="signal">done</field>
          </record>
      </data>
  </odoo>
  ```

* 编辑模板

  ```python
  <odoo>
      <data>
           <template id="listing">
             <ul>
               <li t-foreach="objects" t-as="object">
                 <a t-attf-href="#{ root }/objects/#{ object.id }">
                   <t t-esc="object.display_name"/>
                 </a>
               </li>
             </ul>
           </template>
           <template id="object">
             <h1><t t-esc="object.display_name"/></h1>
             <dl>
               <t t-foreach="object._fields" t-as="field">
                 <dt><t t-esc="field"/></dt>
                 <dd><t t-esc="object[field]"/></dd>
               </t>
             </dl>
           </template>
      </data>
  </odoo>
  ```

* 编辑权限（略）

* 启动服务

* 打开开发者模式

* 更新应用列表

* 安装应用

* 源码下载地址:http://code.tlrfid.tl/py/leave.git