zapp：易度应用开发框架
=========================================

易度应用开发框架，是易度企业应用的开源版本。目标：更快的开发企业应用。

- 易度工作平台是基于这个框架开发的
- 这个框架提供了易度扩展应用的线下运行调试环境

主要功能
===============

- 表单
- 流程
- 脚本
- 规则
- 元数据
- 状态
- 日志
- 通知
- 订阅
- 版本
- 索引
- 回收站
- 权限
- 软件包管理：启动自动加载软件包

不包括的内容
====================
- 用户和组管理，必须连到易度系统才能工作
- 多租户运营管理

依赖
===========
- ztq
- zapian
- zope.annotations
- zope.intid
- zope.interface
- zope.security

开发环境
================
- pyramid
- ZODB
- redis
- bootstrap UI

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
        return call_script('zopen.hello.my_add', x, y)

表单
---------------
可以这么来显示一个表单:

    form = Form(TextField(name='asdfa'),
                SelectField(name=''))
    template = form.genTemplate() # 可传入表单样式 div/table
    # 渲染表单
    form =  form.render(template, {}, request, fields.keys(), errors,
                        context=context, container = container)

提交保存表单，可能存在校验:

    results = {}  # 结果保存到这里
    errors = form.save(fields.keys(), results, request, context=context, container=container)

流程
-------------------
