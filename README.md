zapp：易度应用开发框架
=========================================

易度应用开发框架，是易度企业应用的开源版本。目标：更快的开发企业应用。

- 易度工作平台是基于这个框架开发的
- 这个框架提供了易度扩展应用的线下运行调试环境

开发环境： pyramid + ZODB + redis + bootstrap UI

使用介绍
==========================

一个视图
-----------
在apps文件夹中创建一个文件夹, zopen.hello，里面放入views.py:

      @view_config(permission="Public", template="None")
      def hello(context, request):
          return 'hello, world'
        
直接访问 http://server_port/@@@zopen.hello.hello 即可

调用函数
--------------------
在zopen.hello中放入utils.py:

    def my_add(x, y):
        return x+y
       
    def my_add2(x, y):
        return edo_apps.zopen.hello.my_add(x, y)

表单
---------------
可以这么来显示一个表单:

    form = Form(TextField(name='asdfa'),
                SelectField(name=''))
    template = form.render_template(layout='div') # 可传入表单样式 div/table
    # 渲染表单
    form =  form.render(template, data={}, request, fields.keys(), errors,
                        context=context, container = container)

提交保存表单，可能存在校验:

    results = {}  # 结果保存到这里
    errors = form.save(fields.keys(), results, request, context=context, container=container)

流程
-------------------
定义一个流程(流程由表单、步骤、阶段、设置这几部分组成):

    workflow = WorkFlow(form, wf_steps=[], wf_config=[], wf_stages=[])

创建一个流程表单：

    tasks = [] # 当前没有任务，下一行，会自动根据当前任务来渲染可编辑项
    workflow.render(form, data=None, tasks, request, template, errors)

提交流程表单：

    errors = workflow.save(request, tasks, errors)
    errors = worflow.submit(task, action_name, data, request, as_principal=None, comment="")

基本内容
---------------------------
基本内容包括文件夹Folder和条目Item:

    # 文件夹支持排序
    wf1 = root['wf1'] = Folder()
    item1 = wf1['item1' = Item()
    
唯一ID
---------------------
intid管理，注册，根据id，得到对象

考虑大大数据量，需要支持分区存储

前缀

回收站
------------
所有对象删除进入回收站

需要支持分区存储

索引和搜索
-------------
加入索引，方便搜索

考虑到大数据量，需要支持分区存储

权限管理
--------------------
pid和rol的管理

扩展属性
---------------------------
定义一个扩展属性:

    Metadata(form, )

对象关系
--------------

规则
-----------------------
每个容器可以定义自己的规则，规则可以继承

状态
--------------
每个对象可以包括一组状态

日志
-------------
方便记录对象的日志

通知
-------------
发送通知

订阅
-----------
设置对象的订阅人

版本
-----
所有Item支持版本管理

评论
--------------

软件包管理
-------------------
安装软件包、部署软件包
