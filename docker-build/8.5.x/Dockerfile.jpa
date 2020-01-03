FROM vantoo/websphere:8.5.5.15
#修改JVM参数
RUN sed -i 's/<jvmEntries/<jvmEntries initialHeapSize="512" maximumHeapSize="2048"/g' /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/config/cells/DefaultCell01/nodes/DefaultNode01/servers/server1/server.xml
RUN sed -i 's/genericJvmArguments=""/genericJvmArguments="-server -Xms1g -Xmx2g -XX:NewRatio=1 -XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=512m"/g' /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/config/cells/DefaultCell01/nodes/DefaultNode01/servers/server1/server.xml

#修改默认端口
RUN sed -i 's/WC_defaulthost=9080/WC_defaulthost=9081/g' /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/properties/portdef.props
RUN sed -i 's/port="9080"/port="9081"/g' /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/config/cells/DefaultCell01/nodes/DefaultNode01/serverindex.xml
RUN sed -i 's/port="9080"/port="9081"/g' /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/config/cells/DefaultCell01/virtualhosts.xml

RUN mv /opt/IBM/WebSphere/AppServer/plugins/javax.j2ee.persistence.jar /opt/IBM/WebSphere/AppServer/plugins/javax.j2ee.persistence.jar.bak
ADD javax.j2ee.persistence.jar /opt/IBM/WebSphere/AppServer/plugins/

RUN mkdir -p /home/was/jar
ADD javassist-3.18.1-GA.jar /home/was/jar/

VOLUME /data

ARG USER=was
ARG GROUP=was

USER root
RUN chown -R $USER:$GROUP /data
USER $USER

CMD ["/work/start_server.sh"]