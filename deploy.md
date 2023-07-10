## Развертывание web-приложения в Tomcat с помощью Maven

Самый популярный веб-сервер для веб-приложений на Java — это Apache Tomcat.
И конечно же с помощью Maven можно деплоить war-файлы прямо в локальный или даже удаленный Tomcat-сервер.
Для автоматического деплоя нашего web-приложения нужно

Шаг первый. Мы должны дать доступ Maven’у к Tomcat-серверу.
Для этого открываем файл conf/tomcat-users.xml в директории, где распакован Apache Tomcat,
и добавляем роли manager-gui и manager-script:

<?xml version='1.0' encoding='utf-8'?>
<tomcat-users>
  <role rolename="manager-gui"/>
  <role rolename="manager-script"/>
  <user username="admin" password="admin" roles="manager-gui,manager-script" />
</tomcat-users>

Шаг второй. Разрешаем доступ Maven к Tomcat.
Для этого открываем файл $MAVEN_HOME/conf/settings.xml и добавляем сервер:

<?xml version="1.0" encoding="UTF-8"?>
<settings ...>
  <servers>
	<server>
  	<id>TomcatServer</id>
  	<username>admin</username>
  	<password>admin</password>
	</server>
  </servers>
</settings>

Шаг третий. Добавляем специальный плагин для автоматизированного деплоя нашего приложения в Apache Tomcat.
Плагин называется [tomcat7-maven-plugin](https://tomcat.apache.org/maven-plugin-2.2/):

<build>
    	<plugins>
        	<plugin>
                <groupId>org.apache.tomcat.maven</groupId>
                <artifactId>tomcat7-maven-plugin</artifactId>
                <version>2.2</version>
            	<configuration>
                    <url>http://localhost:8080/manager/text</url>
                    <server>TomcatServer</server>
                	<path>/simpleProject</path>
            	</configuration>
        	</plugin>
    	</plugins>
	</build>
  
  В разделе configuration указываем:

    url — адрес, где запущен Tomcat, и путь к manager/text
    server — id сервера из файла settings.xml
    path — адрес, по которому будет доступно развертываемое приложение

Команды для управления деплоем:
mvn tomcat7:deploy 	Выполнить деплой приложения в Tomcat
mvn tomcat7:undeploy 	Удалить приложение из Tomcat
mvn tomcat7:redeploy 	Передеплоить приложение
