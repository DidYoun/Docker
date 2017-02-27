# Base
FROM tomcat:9-jre8
# Author
MAINTAINER Didier Youn <didier.youn@gmail.com>
# Run
RUN apt-get update && apt-get install -y \
    default-jdk
# Add user admin
ADD ./conf/context.xml /usr/local/tomcat/conf/context.xml
ADD ./conf/tomcat-users.xml /usr/local/tomcat/conf/
ADD ./conf/manager.xml /usr/local/tomcat/conf/Catalina/localhost/manager.xml
# Run tomcat
CMD ["catalina.sh", "run"]