## 配置 Fill Bank
  1. 修改 Foundation_SystemSetting_SystemSettingRecord[MockUpCasinoDB] 数据库, 改为本地的 ESB[8010] 和 RabbitMQ  
  ``` SQL
    UPDATE Foundation_SystemSetting_SystemSettingRecord SET value = 'http://localhost:8010/services/notificationService' where code = 'NOTIFICATION_SERVICE_URL'
    UPDATE Foundation_SystemSetting_SystemSettingRecord SET value = 'amqp://guest:guest@localhost:5672/' where code = 'NOTIFICATION_MESSAGE_QUEUE_URL'
  ```
  2. 修改 ESB 中 notificationService  
  ``` XML
    Path: camp\trunk\build\camp-dist\build\customized-wso2esb\wso2esb-4.8.1\repository\deployment\server\synapse-configs\default\proxy-services
    <endpoint>
        <address uri="rabbitmq:/test?rabbitmq.server.host.name=127.0.0.1&amp;rabbitmq.server.port=5672&amp;rabbitmq.server.user.name=guest&amp;rabbitmq.server.password=guest&amp;rabbitmq.routingKey.name=NotificationServiceFirstLevelMQ&amp;rabbitmq.exchange.name="/>
    </endpoint>
  ```
  3. 重启 ESB, IIS
  4. 启动 Tomcat 检查 ApplicationContext.xml 文件中的 rabbit mq 信息
