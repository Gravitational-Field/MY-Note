## Linux基础知识

### Linux的目录结构



### Linux命令汇总

#### Redis
make
make install
cd /usr/local/   redis被安装到这里了，相当于部署到全局中，环境变量
redis-server 即前台启动服务器端
mkdir /opt/myRedis
将redis.conf复制一份到/opt/myRedis/redis.conf 下
修改/redis.conf   中 daemonize 将no 改为yes，代表后台启动
redis-server  /opt/myRedis/redis.conf    以该配置文件启动

ps -ef | grep redis  查看进程  127.0.0.1 6379
如果已经开启，可以
杀死进程  kill 进程号

redis-cli -h ip地址 -p 6379 shutdown  来关闭客户端与服务端

redis-cli   启动redis客户端
> shutdown     关闭客户端
> exit  退出客户端

info replication 看当前redis的状态


将redis转为Linux的服务：
cd util
./install-server  
	/usr/local/redis/  .conf
	/usr/local/redis/  .log
	/usr/local/redis/data

systemctl status redis_6379
systemctl stop redis_6379
systemctl  start redis_6379
 
修改服务名
vi /etc/init.d/redis_6379