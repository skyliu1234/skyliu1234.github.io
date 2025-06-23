Hello , good day.

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







