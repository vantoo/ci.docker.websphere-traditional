# 构建was镜像
## 进入was的dockerfile目录
`docker-build/9.0.5.0/Dockerfile`
## 使用Dockerfile.ubi构建redHat镜像，或者使用Dockerfile构建ubuntu镜像
[Installation Manager and Packaging Utility download documents](http://www-01.ibm.com/support/docview.wss?uid=swg27025142)
```
docker build -t vantoo/websphere:9.0.5.0 . \
    --build-arg IBMID={IBMid} \
    --build-arg IBMID_PWD={IBMid_password} \
    --build-arg IMURL={IBM_Installation_Manager_download_url}
```

## 换成Dockerfile.jpa(替换了jar并修改端口)
```
docker build -t vantoo/websphere:9.0.5.0-jpa .
```

## 运行镜像
```
docker run --name was9-jpa -v /usr/local/was/PASSWORD:/tmp/PASSWORD \
-v /usr/tmp/was-data/:/data/ \
-e UPDATE_HOSTNAME=true \
-p 9060:9060 -p 9043:9043 -p 9443:9443 -p 9082:9082 \
--restart=always \
-d vantoo/websphere:9.0.5.0-jpa
```