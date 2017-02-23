# Base
FROM tomcat:9-jre8
# Author
MAINTAINER Didier Youn <didier.youn@gmail.com>
# Add user admin
ADD ./conf/tomcat-users.xml /usr/local/tomcat/conf/
ADD ./conf/manager.xml /usr/local/tomcat/conf/Catalina/localhost/manager.xml
# Run tomcat
CMD ["catalina.sh", "run"]