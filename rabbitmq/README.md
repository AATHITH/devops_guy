# Install Rabbitmq

## install dependencies

sudo yum update<br>
sudo yum install epel-release socat -y<br>

## erlang download

rpm --import https://packages.erlang-solutions.com/rpm/erlang_solutions.asc<br>
/etc/yum.repos.d/erlang.repo
```
[erlang-solutions]
name=CentOS $releasever - $basearch - Erlang Solutions
baseurl=https://packages.erlang-solutions.com/rpm/centos/$releasever/$basearch
gpgcheck=1
gpgkey=https://packages.erlang-solutions.com/rpm/erlang_solutions.asc
enabled=1

#### note change the version accordingly

yum install erlang-22.1.8
```
reference: [erlang official website](https://www.erlang-solutions.com/resources/download.html)
## install rmq

#### note change the version accordingly

sudo rpm --import https://github.com/rabbitmq/signing-keys/releases/download/2.0/rabbitmq-release-signing-key.asc<br>
wget https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.7.17/rabbitmq-server-3.7.17-1.el7.noarch.rpm<br>
sudo yum install rabbitmq-server-3.7.17-1.el7.noarch.rpm<br>
download reference:[rmq official website](https://www.rabbitmq.com/download.html)

## Start rmq

sudo systemctl start rabbitmq-server<br>
sudo systemctl status rabbitmq-server<br>
sudo systemctl enable rabbitmq-server<br>

## Enable RabbitMQ Web Management

sudo rabbitmq-plugins enable rabbitmq_management<br>
sudo chown -R rabbitmq:rabbitmq /var/lib/rabbitmq/<br>

#### note change the username & password accordingly

sudo rabbitmqctl add_user Admin01 ChAngEmE321<br>
sudo rabbitmqctl set_user_tags Admin01 administrator<br>
sudo rabbitmqctl set_permissions -p / Admin01 ".*" ".*" ".*"<br>

## check the webui

curl http://Your_Server_IP:15672/ 

(you need to create `/etc/rabbitmq/rabbitmq.conf` to change the config it is not created by default)

Reference links:
[best](https://portal.cloudunboxed.net/knowledgebase/46/How-to-Install-RabbitMQ-Server-on-CentOS-7.html)
[next best](https://gist.github.com/fernandoaleman/fe34e83781f222dfd8533b36a52dddcc)
