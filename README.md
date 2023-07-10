## Создание простого приложения на Java Servlet API

1.  Создадам веб проект из шаблона Maven: [mvn archetype:generate](https://maven.apache.org/archetypes/maven-archetype-webapp/)

2.  В pom.xml добавим зависимость [jakarta.servlet-api](https://mvnrepository.com/artifact/jakarta.servlet/jakarta.servlet-api/6.0.0)

3.  Собрать приложение с помощью: mvn clean package

4.  Запустить Tomcat: tomcat/bin/startup.sh

5.  Копируем *.war файл в директорию tomcat/webapps

6.  To install a JDBC you can copy the [mysql-connector-java-8.0.19.jar](https://dev.mysql.com/downloads/connector/j/) file into %CATALINA_HOME%/lib

[Развертывание проекта с помощью Maven](https://javarush.com/quests/lectures/questservlets.level02.lecture04)
