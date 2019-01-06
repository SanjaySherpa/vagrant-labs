build:
	@docker-compose -p jenkins build
run:
	@docker-compose -p jenkins up -d
stop:
	@docker-compose -p jenkins down
clean-data: 
	@docker-compose -p jenkins down -v


old-clean:
	@docker stop jenkins-master
	@docker stop jenkins-nginx
	@docker rm jenkins-master
	@docker rm jenkins-nginx
	@docker volume rm jenkins-data
	@docker volume rm jenkins-log
	@docker network rm jenkins-net