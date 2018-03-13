## 1.添加用户

我们可以在Odoo设置-&gt;用户 菜单中进行用户的添加或删除管理。

> 在系统中我们添加一个出纳用户A 使之具有对销售和采购的收付款功能。

![](file:///C:\Users\xc\AppData\Roaming\Tencent\Users\419412545\QQ\WinTemp\RichOle\}L%28~9ONRYQ`US3Y%29$7E5{EJ.png)

> 在应用程序中我们去除所有的应用模块，稍后我们将增加自定义的权限菜单

![](file:///C:\Users\xc\AppData\Roaming\Tencent\Users\419412545\QQ\WinTemp\RichOle\H]WDDG}F1P_5W8O49}5F99B.png)

> 点击更改密码，在新密码处点击 输入新密码 以便我们登录该用户。

## 2 添加对应的用户组

> Odoo安装完成后，默认用户组管理功能是不可见的，我们需激活开发模式方可进行管理;在 设置-&gt;激活开发者模式 激活开发模式

![](file:///C:\Users\xc\AppData\Roaming\Tencent\Users\419412545\QQ\WinTemp\RichOle\~I1O2FMQ18DQP$RYONU5JF5.png)

### 2.1 添加出纳用户组

> 激活开发模式，我们可以在设置用户菜单下看到群组功能;点击创建添加

由于创建收付款属于会计功能，在应用程序选择会计，名称为 出纳。在菜单选项卡中我们分别添加以下菜单

![](file:///C:\Users\xc\AppData\Roaming\Tencent\Users\419412545\QQ\WinTemp\RichOle\HQ]44W2GF_[TEH~{}~I[O5V.png)保存后我们将chuna\_a加入出纳用户组。

![](file:///C:\Users\xc\AppData\Roaming\Tencent\Users\419412545\QQ\WinTemp\RichOle\$%29AAWRRZXMD[}6GJKH231XI.png)

登录chuna\_a用户，在菜单 会计中已经有了会计菜单，但还没有收付款菜单，这是因为我们还没有添加收付款菜单的访问权限，下一步我们将添加对应的访问权限。

### 2.2 为菜单添加访问权限

> 添加访问权限时，我们需查询对应菜单视图模型代码。进入会计-&gt;销售 点击调试中的`编辑搜索视图` 复制其中的`模型`代码。

![](file:///C:\Users\xc\AppData\Roaming\Tencent\Users\419412545\QQ\WinTemp\RichOle\XLD[9P40J3Y]4_V5{9GCDA0.png)

![](/assets/import0313.png)编辑`群组` 会计及财务 / 出纳 在选项卡访问权限 点击`添加项目`_对象名及名称为刚才模型代码 ,分别将4个权限勾选上。保存后我们就能在chuna\_a的菜单中看到收付款菜单了。_

![](/assets/import031301.png)

