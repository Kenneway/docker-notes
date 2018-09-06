
# Docker安装MySQL server
********************************************************************************

czj@czj-XPS-8910:~$ mkdir -p ~/docker/mysql/data ~/docker/mysql/logs ~/docker/mysql/conf


czj@czj-XPS-8910:~$ cd ~/docker/mysql


czj@czj-XPS-8910:~/docker/mysql$ sudo docker run -p 3307:3306 --name mysql-server -v $PWD/conf/:/etc/mysql/ -v $PWD/logs:/logs -v $PWD/data:/mysql_data -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.6

	命令说明：

	-p 3307:3306 : 分配宿主机的端口映射到虚拟机上
	
	--name mysql-server : 指定该容器的名称
	
	-v $PWD/conf/:/etc/mysql/ : 将主机的目录挂载到容器的目录上
	
	-v $PWD/logs:/logs : 将主机的目录挂载到容器的目录上
	
	-v $PWD/data:/mysql_data : 将主机的目录挂载到容器的目录上
	
	-e MYSQL_ROOT_PASSWORD=123456 
	
	-d : 后台运行容器，并返回容器ID；
	
	mysql:5.6　: 镜像完整名称


# Docker安装MySQL client
********************************************************************************

sudo docker run -it --link mysql-server --rm mysql:5.6 sh -c 'exec mysql -h "172.18.6.42" -P3307 -uroot -p123456'

sudo docker run -it --name mysql-client --link mysql-server mysql:5.6 sh -c 'exec mysql -h "172.18.6.42" -P3307 -uroot -p123456'

	命令说明：

	-it : 以交互的方式打开并连接伪终端
	
	--link mysql-server : 链接mysql server运行的容器
	
	--rm　: 容器关闭后自动删除
	
	mysql:5.6 : 镜像完整名称
	
	sh -c 'exec mysql -h "172.18.6.42" -P3307 -uroot -p123456' : 执行命令


错误命令：
sudo docker run -it --name mysql-client --link mysql-server mysql:5.6 sh -c 'exec mysql -P3307 -uroot -p123456'

报错如下：
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2)

分析：
mysql -h "172.18.6.42" -P3307 -uroot -p123456
mysql -P3307 -uroot -p123456
？若不指定主机，只改变端口号不能切换数据库？