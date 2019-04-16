**这是一个用tp5框架写的auth权限功能模块的demo 可以给一些基础小白借鉴**


一、 数据库表关系的解释,,三张固定表,一张自建的用户表（数据库文件在demo中导入即可）

_`auth最复杂的就是这个数据表,理解了数据表就理解一半了，这里给大家说明一下，理理逻辑`_


1.**think_auth_group_access**{ //中间表  用户表和等级表的绑定

    uid          --------  这个是用来保存用户表的主键id
    group_id     --------  这个是用来保存等级表的主键id
    
}



2.**think_user**{ //用户表 自己创建的表

    id           --------  用户表的主键id
    user_name    --------  用户名
}


3.**think_auth_group**{  //等级表 可以理解用户会员等级表

    id           --------  等级表的主键id
    title        --------  等级名称
    status       --------  状态
    rules        --------  绑定操作表的主键id 存储方式为 1,2,3 代表有三条操作的权限
    
}

3.**think_auth_rule**{ //操作权限表 用于存储操作
    
      id           --------  操作权限表的主键id
      name         --------  存储操作的url路径
      title        --------  存储操作的url路径的名称
      type         --------  类型 如果是1 的话 就执行condition定义的规则
      status       --------  状态
      condition    --------  用于加入正则的权限规则条件 是需要自己添加正则条件的

}
_`表的字段分析完了,逻辑是这样的：中间表取用户的id到等级表找到他的等级，
再根据他的等级id找到对应的 rules字段 存储的操作权限表的id到操作权限表找到这个等级可以使用的权限判断是否拥有权限，就是这么简单`_










**二、index模块的控制器文件介绍，可以自行挨个访问里面的方法演示**

_`由于tp5没有自带的auth验证类，所以把tp3.2的auth工具类兼容丢进了tp5的工具类里
（在根目录的extend/org/Auth.php）需要到该文件把“默认配置”的东西改成自己对应的数据库表`_


      index.php    --------  写了一个超级简单的调用auth的demo演示
      
      indextwo.php --------  写了auth权限验证的各种方法调用演示
     
