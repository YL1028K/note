# Docker学习笔记

**从入门到实践** https://yeasy.gitbook.io/docker_practice/

## 1.1 常用命令

```shell
docker image ls
docker ps -a

#启动容器
docker run -dit --name test03 r.duxiaoman-int.com/base/centos:7.3.1611-dxm-2021042601 /bin/bash
#进入容器
docker exec -it  test03 /bin/bash
docker exec -it  test02 /bin/bash

#启停容器
docker stop 1e560fca3906|test1
docker restart 1e560fca3906
docker start 1e560fca3906 

#删除容器
docker rm -f 1e560fca3906
```

