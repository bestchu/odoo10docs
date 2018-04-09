## Odoo10配置文件详解

```ini
[options]  
; addons模块的查找路径  
addons_path = E:\GreenOdoo8.0\source\openerp\addons  
; 管理员主控密码(用于创建、还原和备份数据库等操作)  
admin_passwd = admin  
; 自动重载?  
auto_reload = None  
; 用于导入导出的csv文件的默认分隔符  
csv_internal_sep = ,  
; data目录, 用于存放session信息、附件  
data_dir = data  
; 数据库主机名  
db_host = 127.0.0.1  
; 数据库的最大连接数  
db_maxconn = 64  
; 指定要使用的数据库名  
db_name = False  
; 数据库用户密码  
db_password = openerp  
; 数据库端口号  
db_port = 65432  
; 创建新数据库时使用的数据库模板  
db_template = template1  
; 数据库用户名  
db_user = openerp  
; 过滤要显示的数据库名称  
dbfilter = .*  
; 是否为调试模式  
debug_mode = False  
; 哪些模块加载demo数据?  
demo = {}  
; 用于发送邮件的邮箱地址  
email_from = False  
; 在导入大量数据时使用这个选项, 如果在导入期间程序宕机, 你可以在当前状态下继续。指定一个存储中间导入状态的文件名。  
import_partial =   
; 一个处理器允许使用的最大物理内存  
limit_memory_hard = None  
; 一个处理器允许使用的最大虚拟内存  
limit_memory_soft = None  
; 一个处理器接受的最大请求数  
limit_request = None  
; 一个请求最多占用多少处理器时间  
limit_time_cpu = None  
; 一个请求允许的最长实时时间  
limit_time_real = None  
; 是否允许显示数据库列表  
list_db = True  
; 是否将log写入db的ir_logging表  
log_db = False  
; 可以是一组module:log_level对, 默认值是:INFO(表示所有模块的默认日志级别为INFO级别)  
log_handler = :INFO  
; 日志的级别, 可选值包括debug_rpc_answer, debug_rpc, debug, debug_sql, info, warn, error, critical  
log_level = info  
; 指定用来存储日志的文件  
logfile = openerp-server.log  
; 是否按天存放日志  
logrotate = False  
; 长连接池使用的端口号?  
longpolling_port = 8072  
; 处理当前计划任务的最大线程数  
max_cron_threads = 2  
; 强制保存在virtual osv_memory表中的记录的最长时间，以小时为单位  
osv_memory_age_limit = 1.0  
; 强制一个virtual osv_memory表的最大记录数  
osv_memory_count_limit = False  
; 数据库可执行文件的路径  
pg_path = runtime/pgsql/bin  
; 存储服务器pid的文件名  
pidfile = None  
; 是否使用反向代理模式  
proxy_mode = False  
; 是否压缩报表  
reportgz = False  
; 指定用于SSL连接的证书文件  
secure_cert_file = server.cert  
; 指定用于SSL连接的主密钥文件  
secure_pkey_file = server.pkey  
; server范围的模块,以逗号分隔  
server_wide_modules = None  
; 发送邮件的SMTP用户密码  
smtp_password = False  
; SMTP端口号  
smtp_port = 25  
; SMTP服务器名  
smtp_server = localhost  
; SMTP服务器是否支持SSL协议  
smtp_ssl = False  
; 发送邮件的SMTP用户名  
smtp_user = False  
; 是否把日志发送给系统日志服务器  
syslog = False  
; 是否提交YAML或XML测试造成的数据库更改  
test_commit = False  
; 是否允许YAML和单元测试  
test_enable = False  
; YML测试文件  
test_file = False  
; 报表的范例的存放位置  
test_report_directory = False  
; 为系统提供一个参照的时区  
timezone = False  
; 哪些模块可翻译, 默认为all  
translate_modules = ['all']  
; 是否使用数据库的unaccent功能  
unaccent = False  
; 在安装时哪些模块不加载演示数据  
without_demo = False  
; 要使用的处理器数量  
workers = None  
; 是否允许使用XML-RPC协议，默认为True  
xmlrpc = True  
; 指定使用XML-RPC协议的IP地址，为空时表示绑定到现有IP  
xmlrpc_interface =   
; XML-RPC协议使用的TCP端口  
xmlrpc_port = 8069  
; 是否允许使用XML-RPC安全协议，默认为True  
xmlrpcs = True; 指定使用XML-RPC安全协议的IP地址，为空时表示绑定到现有IPxmlrpcs_interface = ; XML-RPC安全协议使用的TCP端口xmlrpcs_port = 8071  
```

