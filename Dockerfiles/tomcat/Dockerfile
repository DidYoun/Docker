# Base
FROM tomcat:9-jre8
# Author
MAINTAINER Didier Youn <didier.youn@gmail.com>
# Run
RUN apt-get update && apt-get install -y \
    openjdk-8-jdk
# Add user admin
ADD ./conf/context.xml /usr/local/tomcat/conf/context.xml
ADD ./conf/tomcat-users.xml /usr/local/tomcat/conf/
ADD ./conf/manager.xml /usr/local/tomcat/conf/Catalina/localhost/manager.xml
ADD ./lib/mysql-connector-java-5.1.41-bin.jar /usr/local/tomcat/lib
# Run tomcat
CMD ["catalina.sh", "run"]