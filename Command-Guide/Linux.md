**GIT STARTUP**

**CMD**
- cd /opt/docker/docker-compose/camp-all
- docker-compose ps    // 查看容器状态
- docker-compose xxx start   // 启动 xxx 容器
- docker-compose xxx stop   // 停止 xxx 容器
- docker logs camp-is   // 查看log
- docker logs -f --tail=1000 camp-is   // 查看实时log
- docker exec -it 1d19e40b18e2 /bin/bash   // 进入docker 容器
- docker cp /opt/build/customized-wso2ei-esb/customization/repository/deployment/server/carbonapps/ 1d19e40b18e2:/home/wso2carbon/wso2ei-6.5.0/wso2/tmp/carbonapps/-1234/   // 从ubuntu拷贝文件到某个容器
- cat xxx   // 查看xxx log
- tail -f xxx.log | grep 'filter1' | grep 'filter2'  // 关键字过滤
- tail -f wso2carbon.log | grep 'BB0202'
- tail -n 1000 wso2carbon.log | grep '09:4'  // 前一千行
- sudo rm -rf ./customized-wso2ei-esb
- sudo chmod -R 777 ./customized-wso2ei-esb

