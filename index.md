# Hello , good day.

# VPS的环境

## VPS prepare

www.vultr.com

直接注册帐号,然后再申请虚拟主机,获取到IP后再测试是否能Ping通,

如果不通,则在申请个虚拟主机,直到申请可用的IP,然后再把前面的删除.

## 注册域名

   https://www.namesilo.com/
   .com域名太贵,可以注册个.top域名

   这个主要给websocket方式的v2ray是用.DNS解析.

## v2ray install

- ubuntu  apt-get update -y && apt-get install curl -y
  centos yum update -y && yum install curl -y

- bash <(curl -s -L https://git.io/v2ray.sh)

- V2Ray 客户端使用教程: https://233v2.com/post/4/

  (v2rayN.exe)ou

-  提示: 输入 v2ray url 可生成 vmess URL 链接 / 输入 v2ray qr 可生成二维码链接



## CloudFlare

-    www.cloudflare.com

     可以隐藏想访问的IP,通过CF代理.

     需要配置域名解析.并在域名提供商配置DNS解析服务器

  > cory.ns.cloudflare.com
  >
  > mimi.ns.cloudflare.com



------

# OpenGrok 

## opengrok.sh

```
#!/bin/bash
case ${1} in
    "run")
        if [[ $2 != '' ]]
        then
            sudo docker run -d \
	        --name opengrok \
	        -p 8080:8080/tcp \
	        -e SYNC_PERIOD_MINUTES="60" \
	        -v ${2}:/opengrok/src/ \
	        -v ~/opengrok/etc/:/opengrok/etc/ \
	        -v ~/opengrok/data/:/opengrok/data/ \
	        opengrok/docker:1.13.25
        else
            sudo docker run -d \
	        --name opengrok \
	        -p 8080:8080/tcp \
	        -e SYNC_PERIOD_MINUTES="60" \
	        -v ~/opengrok/src:/opengrok/src/ \
	        -v ~/opengrok/etc/:/opengrok/etc/ \
	        -v ~/opengrok/data/:/opengrok/data/ \
	        opengrok/docker:1.13.25
        fi
    ;;
    "del")
        sudo docker stop opengrok
        sudo docker rm opengrok
    ;;
    "restart")
        sudo docker restart opengrok
    ;;
    "update-index")
        sudo docker exec -it opengrok opengrok-indexer \
        -J=-Djava.util.logging.config.file=/opengrok/etc/logging.properties \
        -a /opengrok/lib/opengrok.jar -- \
        -c /usr/local/bin/ctags \
        -s /opengrok/src -d /opengrok/data -H -P -S -G \
        -W /opengrok/etc/configuration.xml
    ;;
    "docker-install")
        sudo apt-get install docker.io
        sudo docker --version
        sudo docker pull swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/opengrok/docker:1.13.25
        sudo docker tag swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/opengrok/docker:1.13.25 docker.io/opengrok/docker:1.13.25
    ;;
    "createdir")
        mkdir -p ~/opengrok/{src,etc,data,dist}
    ;;
    "help")
        echo "createdir"
        echo "docker-install"
        echo "run [sourcedir] :for example run ~/sz_trunk/projects"
        echo "del"
        echo "restart"
        echo "update-index"
    ;;
    "")
        echo "createdir"
        echo "docker-install"
        echo "run [sourcedir] :for example run ~/sz_trunk/projects"
        echo "del"
        echo "restart"
        echo "update-index"
    ;;

esac


```

## Docker install

Ubuntu

```
sudo apt-get install docker.io
sudo docker --version
```



Pull OpenGrok 国内镜像

```
sudo docker pull swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/opengrok/docker:1.13.25
sudo docker tag swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/opengrok/docker:1.13.25 docker.io/opengrok/docker:1.13.25
```



## OpenGrok Install

- prepare dir

  ```
  mkdir -p ~/opengrok/{src,etc,data,dist}
  ```

  

- run OpenGrok Container

  ```
   sudo docker run -d \
  	        --name opengrok \
  	        -p 8080:8080/tcp \
  	        -e SYNC_PERIOD_MINUTES="60" \
  	        -v ~/opengrok/src:/opengrok/src/ \
  	        -v ~/opengrok/etc/:/opengrok/etc/ \
  	        -v ~/opengrok/data/:/opengrok/data/ \
  	        opengrok/docker:1.13.25
  ```

  

- update index

  ```
  sudo docker exec -it opengrok opengrok-indexer \
          -J=-Djava.util.logging.config.file=/opengrok/etc/logging.properties \
          -a /opengrok/lib/opengrok.jar -- \
          -c /usr/local/bin/ctags \
          -s /opengrok/src -d /opengrok/data -H -P -S -G \
          -W /opengrok/etc/configuration.xml
  ```

  

- restart OpenGrok

  

  ```
  sudo docker restart opengrok
  ```

  

- Notice

  ```
  repo project
  you should repo start local_branch --all to create the local branch
  the project shoud put in the ~/opengrok/src which you bind
  For example:
  ~/opengrok/src/project1/.git
  ~/opengrok/src/project2/.git
  ~/opengrok/src/ffmepg/.git
  
  ```



------

