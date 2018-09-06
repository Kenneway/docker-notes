# Docker设置openface的开发环境
********************************************************************************

czj@czj-XPS-8910:~$ mkdir ~/docker/new_openface
czj@czj-XPS-8910:~$ 

czj@czj-XPS-8910:~/docker/new_openface$ sudo docker run --name openface -p 9000:9000 -p 8000:8000 -v $PWD:/root/new_openface/ -it bamos/openface /bin/bash

	命令说明：

	--name openface : 指定该容器的名称
	
	-p 9000:9000 : 分配宿主机的端口映射到虚拟机上
	
	-v $PWD:/root/new_openface/ : 将主机的目录挂载到容器的目录上
	
	-it : 以交互的方式打开并连接伪终端
	
	bamos/openface　: 镜像完整名称

	/bin/bash : 容器执行命令启动一个shell

root@9f1e9232fffc:~# cp -rf ~/openface/* ~/new_openface/

czj@czj-XPS-8910:~/docker/new_openface$ sudo chown -R czj:czj ./*

********************************************************************************


