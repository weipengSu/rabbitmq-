# rabbitmq的搭建和实战
rabbitmq  基于linux centos7 版本进行的搭建

1: 如果以前安装过erlang or rabbitmq or socat请先下载，不然安装新版本可能会和老版本冲突
删除erlang： rpm -qa | grep erlang | xargs rpm -e --nodeps
删除rabbitmq:   rpm -qa | grep rabbitmq | xargs rpm -e --nodeps
删除socat:  rpm -qa | grep socat | xargs rpm -e --nodeps


2: 删除完毕开始安装
安装erlang：    sudo yum install erlang
安装socat:      sudo yum install socat
安装rabbitmq:   sudo yum install rabbitmq

3:安装完成后 
$ sudo chkconfig rabbitmq-server on  # 添加开机启动RabbitMQ服务
$ sudo /sbin/service rabbitmq-server start # 启动服务
$ sudo /sbin/service rabbitmq-server status  # 查看服务状态
$ sudo /sbin/service rabbitmq-server stop   # 停止服务

# 查看当前所有用户
$ sudo rabbitmqctl list_users

# 查看默认guest用户的权限
$ sudo rabbitmqctl list_user_permissions guest

# 由于RabbitMQ默认的账号用户名和密码都是guest。为了安全起见, 先删掉默认用户
$ sudo rabbitmqctl delete_user guest

# 添加新用户                  # 自己设置下username 和password
$ sudo rabbitmqctl add_user username password

# 设置用户tag                     # 刚自己设置的username
$ sudo rabbitmqctl set_user_tags username administrator

# 赋予用户默认vhost的全部操作权限     # 刚设置的 password 和 username
$ sudo rabbitmqctl set_permissions -p / username ".*" ".*" ".*"

# 查看用户的权限                          # 刚自己设置的username
$ sudo rabbitmqctl list_user_permissions username

# 可以去修改也可以不去修改
# 修改用户的密码 
$ rabbitmqctl  change_password  Username  'Newpassword'

4：开启web可视化页面
sudo rabbitmq-plugins enable rabbitmq_management

5: 在本地浏览器直接
http://+ip:15672出现可视化界面即可

原文链接：https://blog.csdn.net/yu_hongrun/article/details/107571829

