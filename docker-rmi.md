
	sudo rmi IMAGE_ID
	
删除指定的镜像

	sudo docker rmi $(sudo docker images -qf dd=true)
	
删除所有未打dd标签的镜像

	sudo docker rmi $(sudo docker images -q)
	
删除所有镜像