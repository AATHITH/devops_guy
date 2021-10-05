# REDIS
This page will walk you through 
1. How to install,
2. Run/Stop/Restart
3. How to configure Redis with Sentinel
4. How to run it with systemd
5. How to upgrade to latest version
6. Uninstall Redis Server

## 1. How to install:
<details>
<summary>Ubuntu</summary>
<br>
```
sudo apt-get update 
sudo apt-get install build-essential tcl8.5
wget http://download.redis.io/releases/redis-stable.tar.gz
tar xzvf redis-stable.tar.gz
cd redis-stable
make
make test
sudo make install
cd utils
sudo ./install_server.sh
sudo service redis_6379 start
```
</details>
### 2. Start|Stop|Restart Redis:
You can start/stop/restart Redis in multiple ways,
|ACTION|COMMAND|
|--|--|
|start| sudo service redis start<br>redis-server /path/to/redis.conf<br>/usr/local/bin/redis-server start<br>/etc/init.d/redis_6379 start<br>redis-server /usr/local/etc/redis/6379.conf start|
|stop|sudo service redis stop<br>redis-cli shutdown<br>/usr/local/bin/redis-server stop<br>/etc/init.d/redis_6379 stop<br>redis-server /usr/local/etc/redis/6379.conf stop|
|restart|sudo service redis restart<br>/usr/local/bin/redis-server start/stop/restart|

### Check Redis is running:
`ps aux | grep redis-server` or `sudo service redis_6379 status`

**Run redis as daemon:** ` redis-server --daemonize yes`

**Run Redis on different port:** `redis-server --port 6380`

**3. Run sentinel as service:** This [link](https://gist.github.com/DeviaVir/5431730) will help you run Sentinel as a service 

**Passing arguments via the command line:**
`redis-server --port 6380 --slaveof 127.0.0.1 6379`

**To remove old Sentinels from configurations:**
(Old sentinels are not removed from configuration. So, you have to manually edit your configurations) 
`SENTINEL RESET mymaster`

**Returns list of master:** `${SERVER_IP}:26379> sentinel slaves redis-cluster`

**Initiate failover:**`${SERVER_IP}:26379> sentinel master  redis-cluster`

**Binding rules:** 
You cannot have bind 127.0.0.1 123.123.123.123 but bind 123.123.123.123 127.0.0.1 in your sentinel.conf.
sentinel auth-pass redis-01 password 

## How to upgrade to latest version
(this example is for upgrading redis 5.0.8 to redis 6.2.6 on Centos7)
#### To backup existing redis instance:
```
cd /usr/bin/
mv redis-benchmark redis-benchmark_v5 mv redis-check-aof redis-check-aof_v5 mv redis-check-rdb redis-check-rdb_v5 mv redis-cli redis-cli_v5 mv redis-sentinel redis-sentinel_v5 mv redis-server redis-server_v5
ln -sfn redis-server_v5 redis-check-aof_v5 ln -sfn redis-server_v5 redis-check-rdb_v5 ln -sfn redis-server_v5 redis-sentinel_v5
```
**INSTALL WITH SOURCE:**
To Install the updated Redis:
```
yum install systemd-devel
wget http://download.redis.io/releases/redis-6.2.6.tar.gz
tar xzf redis-6.2.6.tar.gz
cd redis-6.2.6
make BUILD_WITH_SYSTEMD=yes USE_SYSTEMD=yes   #to make redis work with systemd
sudo cp /home/deploy/redis-6.2.6/src/{redis-cli,redis-check-rdb,redis-server,redis-sentinel,redis-check-aof,redis-benchmark,redis-trib.rb} /usr/bin/
systemctl restart redis
redis-server --version
```
**WITH YUM:**  	https://computingforgeeks.com/how-to-install-latest-redis-on-centos-7/
```
sudo yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
sudo yum --enablerepo=remi list redis
sudo yum --enablerepo=remi install redis
redis-cli -p 26379 info
```
## uninstall redis:

    sudo -i
    service redis-server stop
    apt remove --purge redis-server
    rm /var/lib/redis/dump.rdb
    apt install redis-server
    systemctl enable redis-server
    service redis-server start

I have not tried, but it is possible this is enough

    service redis-server stop
    rm /var/lib/redis/dump.rdb
    service redis-server start


### Reference links:
**standalone:**
[redis sentinel high availability(medium)](https://medium.com/@amila922/redis-sentinel-high-availability-everything-you-need-to-know-from-dev-to-prod-complete-guide-deb198e70ea6)

[how to install and use redis(digitalocean)](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-redis)

[how to install and use redis(pivotal)](https://community.pivotal.io/s/article/How-to-install-and-use-Redis-on-Linux)

**master-slave:**
[Setup Redis master and slave(pivotal)](https://community.pivotal.io/s/article/How-to-setup-Redis-master-and-slave-replication)

**sentinel:**
[master slave replication and redis sentinel(RTFM)](https://rtfm.co.ua/en/redis-replication-part-2-master-slave-replication-and-redis-sentinel/)


(This page is created by AATHITH(myself) for my self-reference only.)
