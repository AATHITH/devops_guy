Sync MongoDB with ElasticSearch with Monstache
(This tutorial expects a running instance of Elasticsearch)

# Setup Mongodb
1. Download mongodb from the release page.

`wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-4.4.1.tgz`

2. untar the downloaded file

`tar xzf mongodb-linux-x86_64-rhel70-4.4.1.tgz`

3. CD into the resulted directory

`cd mongodb-linux-x86_64-rhel70-4.4.1/`

4. Copy the mongodb binaries to system bin folder

`cp bin/* /usr/bin/`

5. Create a dir for mongodb data

`mkdir -p /var/lib/mongodb1/`

6. Start and run Mongod in background

`mongod --fork --logpath /var/log/mongod1.log --port 27017 --dbpath /var/lib/mongodb1 --replSet rs0`

To run more Mongo instances in same VPS.

7. Create a new directory for another mongo instance

`mkdir -p /var/lib/mongodb2/`

8. Start second instance in different port and data path

`mongod --fork --logpath /var/log/mongod1.log --port 27018 --dbpath /var/lib/mongodb2 --replSet rs0`

9. Connect using 'mongo' client and initiate replication and add the second into the cluster

```
 mongo
 > rs.initiate()
 > rs.add('localhost:27018') # { "ok"" 1 }
 > rs.status()
```
# Monstache Setup
1. Download Monstache & upzip

```
wget https://github.com/rwynn/monstache/archive/v6.7.0.zip
unzip v6.7.0.zip
```
2. CD into the resulted directory

`cd monstache-6.7.0/`

3. Add the monstache (unzipped result dir) to PATH

`export PATH=$PATH:/root/monstache-6.7.0/`

4. check

`monstache -v`

5. create monstache conf file(in .toml)

`{Any path}/config.toml`
```
mongo-url = "mongodb://localhost:27017"
elasticsearch-urls = ["http://localhost:9200"]
elasticsearch-max-conns = 4
elasticsearch-max-seconds = 5
elasticsearch-max-bytes = 8000000

gzip = true
stats = false
index-stats = true

dropped-collections = false
dropped-databases = false

replay = false
resume = true
resume-write-unsafe = false
resume-name = "default"
verbose = true
exit-after-direct-reads = false

[logs]
info = "/var/logs/monstache/info.log"
warn = "/var/logs/monstache/warn.log"
error = "/var/logs/monstache/error.log"
trace = "/var/logs/monstache/trace.log"
```

6. Start Monstache

`monstache -f config.toml`

### Check Sync by doing operations in mongodb

7. Insterting docs in db= new, collection=name.

```
rs0:PRIMARY> use new
switched to db new
rs0:PRIMARY> db.name.insert({"name":"frank"})
WriteResult({ "nInserted" : 1 })
rs0:PRIMARY> db.name.insert({"name":"monica"})
WriteResult({ "nInserted" : 1 })
rs0:PRIMARY> db.name.insert({"name":"frank", "second":"gallagher"})
WriteResult({ "nInserted" : 1 })
```
monstache will output the logs for the above events.
A new index named new.name(dbname.collection) will be created in Elasticsearch.



Reference links:

Full: https://molla4455.gitbook.io/dev-log/elastic/migration

Checking version compactibility: https://rwynn.github.io/monstache-site/start/#which-version-should-i-use

Monstache config explanations: https://partners-intl.aliyun.com/help/doc-detail/171650.htm , https://rwynn.github.io/monstache-site/config/

other useful links: https://medium.com/@nehajirafe/mongodb-to-elasticsearch-sync-using-monstache-cfe1177594b6 , https://medium.com/@aecheverry/mongodb-real-time-sync-with-elastisearch-using-monstache-in-docker-a35cc2bf721a
