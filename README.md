# 快速开始

## EQBoot介绍

![logo](http://stke7hubl.hd-bkt.clouddn.com/Fo0PIS8o6bt-2rIZTJ6wzHGhBeq5)

+ EQBoot是一个基于SpringBoot3.x的快速开发的框架，帮助开发者快速搭建基于的Web应用。 
+ 技术栈: SpringBoot + SpringSecurity + JWT + Mysql + RabbitMQ + Redis + 七牛云

+ 开源地址 : 📂 https://github.com/123asdasdnk/EQBoot
+ 问题反馈 : 👍  https://github.com/123asdasdnk/EQBoot/issues
<hr>

## 环境准备

+ JDK 17
+ Mysql 5.7+
+ Redis  5.0+
+ RabbitMQ 4.0+

其它版本我没有测试过，希望大家可以提供反馈

<hr>

## 快速启动项目

0. 先进入项目地址https://github.com/123asdasdnk/EQBoot, 点上star，支持一下作者，谢谢！

1. 克隆项目到本地

```shell
git clone https://github.com/123asdasdnk/EQBoot.git
```
(当然了，你也可以直接下载压缩包)

2. 解压项目，使用Idea打开
    这里就不用细讲了吧😂

3. 初始化 MySQL
   + 先创建一个名称为springboottemplatepro的mysql数据库 
   + 找到sql文件夹下的account.sql脚本，运行这个脚本来创建用户表
   当然也可以直接运行下面这段sql语句

```sql
    create table db_account
    (
        id            int auto_increment
        primary key,
        username      varchar(255)                 null,
        password      varchar(255)                 null,
        nickname      varchar(255) default 'hello' null,
        email         varchar(255)                 null,
        role          varchar(255) default 'user'  null,
        register_time datetime                     null,
        status        varchar(255) default '否'    null,
        avatar_url    longtext                     null,
        constraint email
        unique (email),
        constraint username
        unique (username)
    );
 ```
4. 启动Redis和RabbitMQ
    + 启动你的Redis服务器
    + 启动你的RabbitMQ，使用默认账号登录(username: admin, password: admin)创建一个名称为/test的虚拟主机

5. 修改配置文件

    找到application.yml配置文件，填写对应的配置

    ``` yml
     code: #验证码模块
       codeLength: 5                  #验证码长度
       codeExpire: 5                  #验证码过期时间
       senderEmail: your_email@qq.com  # 验证码发送端邮箱
    ```
    
    ``` yml
     mail: #邮箱配置
       host: smtp.163.com           # 163邮箱的地址为smtp.163.com，直接填写即可
       username: your_email@163.com # 你申请的163邮箱
       password: your_password      # 注意密码是在开启smtp/pop3时自动生成的，记得保存一下，不然就找不到了，例如：MSBJFHALFUAALFBV(这是我乱输的，用不了)
    ```
   
    ``` yml
     datasource: #数据库
       url: jdbc:mysql://localhost:3306/springboottemplatepro?serverTimezone=UTC&useSSL=false&allowMultiQueries=true&allowPublicKeyRetrieval=true #本地用这个
       username: root # 数据库用户名
       password: your_password # 数据库密码
       driver-class-name: com.mysql.cj.jdbc.Driver # 数据库驱动
    ```
   
    ``` yml
     rabbitmq: #消息队列配置 #要使用就先开启rabbitmq服务，在把这个配置取消注释
       host: 127.0.0.1
       port: 5672
       username: admin
       password: admin
       virtual-host: /test # 如果你不想用/test，你就自己换成你自己的虚拟主机
   ```
   
   ``` yml
    # 七牛云配置，这个配置写在qiniuyun.yml中(这个你可以改，下面这个配置是作者为了方便使用者而提供的，如果要使用，请不要上传违规内容，否则后果自负)
     qiniu: 
       access-key: YjjR9MZt55solE9T9_jK0nLuEPls2f6YQS_OM9V3 # 你的access-key
       secret-key: TfZqWC-EyHOunCbn0ollO_ANzeor9dbTMsvPvXzr # 你的secret-key
       bucket: eqboot # 你的bucket名
       domain: stke7hubl.hd-bkt.clouddn.com # 你的域名
   ```
6. 启动项目
    + 启动TemplateProApplication.java，等待项目启动
    当你看见这个页面就说明启动成功了 🤪
   
    ![效果图](http://stke7hubl.hd-bkt.clouddn.com/FvdXZ-ecU01meongmeF5E1Mfkepr)

<hr>
    
# 项目结构
        
![项目结构](http://stke7hubl.hd-bkt.clouddn.com/FtC3scUCWO_Hem-dcgG8jzVp6lx9)
 + AOP: 用于日志切片
 + config: 各种配置
 + controller: 控制器层，负责处理请求
 + entity: 实体类
 + file: 文件模块
 + filter: 过滤器
 + mapper: 数据库映射类
 + mq: 消息队列模块
 + service: 服务层，负责处理业务逻辑
 + socket: 网络通讯模块(还在开发中)
 + sql: 数据库脚本
 + system: 系统控制模块，用于整个系统的监控
 + task: 定时任务模块
 + utils: 工具类


 




