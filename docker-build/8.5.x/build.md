# 构建was镜像
## 进入was的dockerfile目录
`docker-build/8.5.x/Dockerfile`

## 使用Dockerfile
[Installation Manager and Packaging Utility download documents](http://www-01.ibm.com/support/docview.wss?uid=swg27025142)
```
docker build -t vantoo/websphere:8.5.5.15 . \
    --build-arg IBMID={IBMid} \
    --build-arg IBMID_PWD={IBMid_password} \
    --build-arg IMURL={IBM_Installation_Manager_download_url}
```

## 换成Dockerfile.jpa(替换了jar并修改端口)
```
docker build -t vantoo/websphere:8.5.5.15-jpa .
```

## 运行镜像
```
docker run --name was8.5-jpa -v /usr/local/was/PASSWORD:/tmp/PASSWORD \
-v /usr/tmp/was-data:/data \
-e UPDATE_HOSTNAME=true \
-p 9060:9060 -p 9043:9043 -p 9443:9443 -p 9081:9081 \
--restart=always \
-d vantoo/websphere:8.5.5.15-jpa
```

## 删除缓存目录
```
docker exec was8.5-jpa bash -c "rm -rf /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/temp/wscache/ams_war/ && rm -rf /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/temp/DefaultNode01/server1/ams_war/"
```

## war目录
```
/opt/IBM/WebSphere/AppServer/profiles/AppSrv01/installedApps/DefaultCell01/xxx_war.ear/xxx.war
```
