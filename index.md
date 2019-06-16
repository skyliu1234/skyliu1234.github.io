<<<<<<< HEAD
Hello, let's start thinking and learning 

##  start install shadowsocks
sudo add-apt-repository ppa:hzwhuang/ss-qt5  
sudo apt-get update  
sudo apt-get install shadowsocks-qt5  

install polipo   
sudo apt-get install polipo  
cd /etc/polipo/  
sudo vim config  

add the below text  
socksParentProxy="localhost:1080"  
socksProxyType=socks5  


sudo service polipo stop  
sudo service polipo start  


vim ~/.bashrc  

add the text below:  
alias hp="http_proxy=http://localhost:8123"  
export http_proxy=http://localhost:8123  


git config --global http.proxy localhost:8123  
=======
Hello, let's start thinking and learning

##  start install shadowsocks
sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install shadowsocks-qt5

install polipo
sudo apt-get install polipo
cd /etc/polipo/
sudo vim config

add the below text
socksParentProxy="localhost:1080"
socksProxyType=socks5


sudo service polipo stop
sudo service polipo start


vim ~/.bashrc

add the text below:
alias hp="http_proxy=http://localhost:8123"
export http_proxy=http://localhost:8123


git config --global http.proxy localhost:8123
>>>>>>> e9a1b736ae7716f4650cc7e1816d611a5a267117
