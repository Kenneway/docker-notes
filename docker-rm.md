
	sudo docker rm CONTAINER_ID
	
删除指定的已停止的容器

	sudo docker rm $(sudo docker ps -aq)
	
删除所有已停止的容器