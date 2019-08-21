FROM vantoo/websphere:8.5.5.15
RUN sed -i 's/<jvmEntries/<jvmEntries initialHeapSize="512" maximumHeapSize="2048"/g' /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/config/cells/DefaultCell01/nodes/DefaultNode01/servers/server1/server.xml
RUN sed -i 's/genericJvmArguments=""/genericJvmArguments="-server -Xms1g -Xmx2g -XX:NewRatio=1 -XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=512m"/g' /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/config/cells/DefaultCell01/nodes/DefaultNode01/servers/server1/server.xml
RUN mv /opt/IBM/WebSphere/AppServer/plugins/javax.j2ee.persistence.jar /opt/IBM/WebSphere/AppServer/plugins/javax.j2ee.persistence.jar.bak
ADD javax.j2ee.persistence.jar /opt/IBM/WebSphere/AppServer/plugins/

RUN mkdir -p /home/was/jar
ADD javassist-3.18.1-GA.jar /home/was/jar/

CMD ["/work/start_server.sh"]