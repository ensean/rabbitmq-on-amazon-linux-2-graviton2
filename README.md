
### Option 1: running with docker image
https://hub.docker.com/_/rabbitmq/
```shell
sudo docker run -d \
--hostname my-rabbit \
--name some-rabbit \
-p 4369:4369 \
-p 5671:5671 \
-p 5672:5672 \
-p 15691:15691 \
-p 15692:15692 \
-p 25672:25672 \
-p 8080:15672 \
-e RABBITMQ_DEFAULT_USER=admin \
-e RABBITMQ_DEFAULT_PASS=2wsx1qaz \
rabbitmq:3-management
```


### Option 2：build and run

1. Prepare env dependencies
```shell
yum install ncurses-compat-libs -y # erlang lib dep
yum install socat -y
yum install docker -y #通过docker方式编译
```


2. build eralng otp dep with docker(build within the host will meet systemd check related error)
```shell
wget https://github.com/rabbitmq/erlang-rpm/archive/refs/tags/v23.2.7.tar.gz
tar -xzvf v23.2.7.tar.gz
cd docker
./build-image-and-rpm.sh 7 --no-cache

# install erlang
rpm -ivh ./build/build-dir-7/RPMS/aarch64/erlang-23.2.7-1.el7.aarch64.rpm
```


3. 下载安装rabbitmq-server
```
wget https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.8.6/rabbitmq-server-3.8.6-1.el7.noarch.rpm
rpm -ivh rabbitmq-server-3.8.6-1.el7.noarch.rpm
```
