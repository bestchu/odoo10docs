### Domain使用场合

* 权限管理中的字段级别
* tree视图的过滤器
* 其它...


[官方开发文档](http://www.odoomk.com/documentation/10.0/reference/orm.html#domain)

[参考资料](https://www.kancloud.cn/yangxunbo/odoo10dev/320706)

## **1）Domain条件表达式规则**

最简单的格式：[('字段','操作符',值)]

例：[('shenqr.user_id','=',uid)]

说明：domain中的单个条件是一个三个元素组成的元组，所以务必加上（）。

元组中第一个是对象的一个column，也就是字段名；元组中第二个是比较运算符“=,!=,>,>=,<,<=,like,ilike,in,not in,child_of,parent_left,parent_right“；（注意：在xml文件中使用时，'>='要用'>='表示,'<='要用'<='表示,'!='最好用'><'表示，'>'最好用'>'表示，'<'最好用'<'表示）。

元组中第三个就是用来比较的值了。多个条件用“|”（or），“&”（and），“！”（no）逻辑运算符链接。逻辑运算符作为前缀放置于条件前面。“|”与“&”必须两个条件链接，“！”对一个条件取反。

默认逻辑运算符为“&”。（注意：在xml文件中使用时，'&'要用'&'表示）

## **2)不带逻辑运算符的简单表达式**

过滤状态为待批：[('state','=','wait_prove')]

过滤状态为草稿、待批：

[('state','in',('draft','wait_prove'))]或者[('state','in',['draft','wait_prove'])]

过滤请假天数大于3天：[('tians','>',3)]

## **3)带逻辑运算符的简单表达式**

假设a,b分别是不带逻辑运算符的简单表达式

a=('state','><','draft')

b=('tians','<=',1)

a and b:[a,b]或['&',a,b]

a or b:['|',a,b]

Eg:请假模块，副经理登录时待审批的请假单（状态是待批，并且请假天数在一天以内）菜单过滤条件：

[('state','=','wait_prove'),('tians','<=',1)]

## **4）带逻辑运算符的稍复杂的表达式**

同上，假设a,b,c分别是不带逻辑运算符的简单表达式

a and b and c:[a,b,c]或则['&','&',a,b,c]

a or b or c:['|','|',a,b,c]

a and b or c:['|','&',a,b,c]

a and(b or c):['&',a,'|',b,c]

Eg:经理待审批的请假单（状态是待批，并且请假天数大于一天，并且是本部门的职员请假单，并且还不包含自己的请假单）菜单过滤条件

[('state','=','wait_prove'),('tians','>',1),('shenqr.user_id','<>',uid),('shenqr.department_id','=',department_id),('shenqr.user_id.groups_id','=',59)]

## **5）带逻辑运算符的更复杂的表达式**

同上，假设a,b,c,e,f,g分别是不带逻辑运算符的简单表达式

(a or b and c)or(d and e):

['|','&','|',a,b,c,'&',d,e,3)]

Eg:总经理待审批的请假单（所有部门副经理或经理状态为待批的请假单，或3天以上部门经理批准过的请假单）菜单过滤条件：

['|','&','|',('shenqr.user_id.groups_id','=',60),('shenqr.user_id.groups_id','=',61),('state','=','wait_prove'),'&',('state','=','depmanager_proved'),('tians','>',3)] (a or b and c)or(d and e)or(f and g)

['|','|','&','|',a,b,c,'&',d,e,'&',f,g]

Eg:总经理全部的请假单（所有部门副经理或经理状态为待批的请假单，或3天以上部门经理批准过的请假单，或3天以上状态为同意或驳回的请假单据）菜单过滤条件：

['|','|','&','|',('shenqr.user_id.groups_id','=',60),('shenqr.user_id.groups_id','=',61),('state','=','wait_prove'),'&',('state','=','depmanager_proved'),('tians','>',3),'&',('state','in',['proved','rejected']),('tians','>',3)]