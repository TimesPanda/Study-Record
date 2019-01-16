## 存储服务器
Go中实现的存储服务器。
- minio - Minio是一个与Amazon S3 API兼容的开源对象存储服务器。
- rclone - “用于云存储的rsync” - Google Drive，Amazon Drive，S3，Dropbox，Backblaze B2，One Drive，Swift，Hubic，Cloudfile ......
- perkeep - Perkeep是您终身的个人存储系统：一种存储，同步，共享，建模和备份内容的方式。
- s3git - 适用于云存储的Git。数据的分布式版本控制。
- storj - 分散的云对象存储，价格合理，易于使用，私密且安全。
- rook - Open，Cloud Native和Universal Distributed Storage。
- longhorn Longhorn是一个通过容器提供的开源持久性块存储服务器。

## 键值存储
Go中实现的键值存储。
- BadgerDB - BadgerDB是一个用pure Go编写的可嵌入，持久，简单和快速的键值（KV）数据库。它意味着成为像RocksDB这样非基于Go的键值存储的高效替代品。
- Biscuit - Biscuit是一个用于AWS基础设施机密的多区域HA键值存储。
- consul - 用于服务发现和配置的分布式一致复制键值存储。
- diskv - 磁盘支持的键值存储。
- etcd - 分布式系统最关键数据的分布式可靠键值存储。
- go-cache - 内存中的密钥：Go的值存储/缓存（类似于Memcached）库，适用于单机应用程序。

## 文件系统
Go中实现的文件系统。
- git-lfs - 用于版本化大文件的Git扩展。
- seaweedfs - SeaweedFS是一个简单且高度可扩展的分布式文件系统，适用于小文件。
- fsnotify - Go的跨平台文件系统通知。
- goofys - 用Go编写的高性能POSIX-ish Amazon S3文件系统。
- go-systemd - 绑定到systemd套接字激活，日志，D-Bus和单元文件。
- gcsfuse - 用于与Google云端存储交互的用户空间文件系统。
- svfs - 基于保险丝的Openstack Swift上的虚拟文件系统。
- afero - Go的FileSystem抽象系统

## 数据库
### Go中实现的数据库。
- BigCache - 用于千兆字节数据的高效键/值缓存。
- bolt - Go的低级键/值数据库。Ben Johnson的这个原始版本已经被CoreOS bbolt标记为unmaintained and forked。
- buntdb - Go的快速，可嵌入，内存中键/值数据库，具有自定义索引和空间支持。
- cache2go - 内存中的键：值缓存，支持基于超时的自动失效。
- cockroach - 可扩展，地理复制的事务数据存储区
- couchcache - 由Couchbase服务器支持的RESTful缓存微服务。
- CovenantSQL - 具有区块链功能的SQL数据库。
- dgraph - 可扩展，分布式，低延迟，高吞吐量图数据库。
- diskv - 本土磁盘支持的键值存储。
- eliasdb - 具有REST API，短语搜索和类似SQL的查询语言的无依赖关系的事务图数据库。
- emitter - 具有时间序列消息存储的可扩展，低延迟，分布式和安全的发布/订阅数据库，适用于物联网，游戏，应用和实时网络。
- forestdb - 转到ForestDB的绑定。
- GCache - 支持可过期缓存，LFU，LRU和ARC的缓存库。
- geocache - 适用于基于地理定位的应用程序的内存缓存。
- go-cache - 内存中的密钥：Go的值存储/缓存（类似于Memcached）库，适用于单机应用程序。
- goleveldb - Go中LevelDB键/值数据库的实现。
- groupcache - Groupcache是​​一个缓存和缓存填充库，在许多情况下用作memcached的替代品。
- Influxdb - 用于指标，事件和实时分析的可扩展数据存储区
- ledisdb - Ledisdb是一个基于LevelDB的高性能NoSQL，如Redis。
- levigo - Levigo是LevelDB的Go包装器。
- moss - Moss是一个简单的LSM键值存储引擎，用100％Go编写。
- noms - 版本化，可分叉，可同步的数据库。
- piladb - 基于堆栈数据结构的轻量级RESTful数据库引擎。
- perst - 从任何PostgreSQL数据库提供RESTful API。
- prometheus - 监控系统和时间序列数据库。
- rqlite - 基于SQLite构建的轻量级分布式关系数据库。
- scribble - 一个小小的平面文件JSON商店。
- tidb - TiDB是一个分布式SQL数据库。灵感来自Google F1的设计。
- tiedot - 由Golang提供支持的NoSQL数据库。
- Tile38 - 具有空间索引和实时地理围栏的地理定位DB。

### 数据库架构迁移。
- darwin - Go的数据库模式演化库
- goose - 数据库迁移工具。您可以通过创建增量SQL或Go脚本来管理数据库的演变。
- gormigrate - Gorm ORM的数据库模式迁移帮助程序。
- migrate - Golang中的数据库迁移处理支持MySQL，PostgreSQL，Cassandra和SQLite。
- pravasan - 简单迁移工具 - 目前用于MySQL但计划很快支持Postgres，SQLite，MongoDB等，
- soda - 用于MySQL，PostgreSQL和SQLite的数据库迁移，创建，ORM等。
- sql-migrate - 数据库迁移工具。允许使用go-bindata将迁移嵌入到应用程序中。

### 数据库工具。
- go-mysql - 一个处理MySQL协议和复制的go工具集。
- go-mysql-elasticsearch - 自动将MySQL数据同步到Elasticsearch。
- kingshard - kingshard是由Golang提供支持的MySQL的高性能代理。
- myreplication - MySql二进制日志复制监听器。支持声明和基于行的复制。
- orchestrator - MySQL复制拓扑管理器和可视化工具
- pgweb - 基于Web的PostgreSQL数据库浏览器
- vitess - vitess提供服务器和工具，便于扩展MySQL数据库以用于大规模Web服务。
- usql - SQL数据库的通用命令行界面

### SQL查询构建器，用于构建和使用SQL的库。
- dat - Go Postgres数据访问工具包
- Dotsql - Go库，可以帮助您将sql文件保存在一个位置并轻松使用它。
- goqu - 一个惯用的SQL构建器和查询库。
- igor - PostgreSQL的抽象层，支持高级功能并使用类似gorm的语法。
- ozzo-dbx - 强大的数据检索方法以及与数据库无关的查询构建功能。
- scaneo - 生成Go代码以将数据库行转换为任意结构。
- sqrl - SQL查询构建器，具有改进性能的Squirrel分支。
- Squirrel - Go库，可帮助您构建SQL查询。
- xo - 基于现有模式定义或支持PostgreSQL，MySQL，SQLite，Oracle和Microsoft SQL Server的自定义查询，为数据库生成惯用Go代码。

## 数据库驱动
### 用于连接和操作数据库的库。

- 关系数据库

  - bgc - 用于BigQuery的数据存储连接。
  - firebirdsql - Go的Firebird RDBMS SQL驱动程序
  - go-adodb - Microsoft ActiveX Object DataBase驱动程序，用于使用database / sql。
  - go-bqstreamer - BigQuery快速和并发流插入。
  - go-mssqldb - go语言的Microsoft MSSQL驱动程序。
  - go-oci8 - 使用database / sql的Oracle驱动程序。
  - go-sql-driver / mysql - Go的MySQL驱动程序。
  - go-sqlite3 - 用于使用database / sql的SQLite3驱动程序。
  - gofreetds Microsoft MSSQL驱动程序。转到FreeTDS的包装器。
  - pgx - PostgreSQL驱动程序支持数据库/ sql之外的功能。
  - pq - 用于数据库/ sql的Pure Go Postgres驱动程序。

- NoSQL数据库
  - aerospike-client-go - Go语言的Aerospike客户端。
  - arangolite - ArangoDB的轻量级golang驱动程序。
  - asc - 用于Aerospike的数据存储连接。
  - cayley - 支持多个后端的图形数据库。
  - dsc - SQL，NoSQL，结构化文件的数据存储连接。
  - dynago - Dynago是DynamoDB最少的意外客户端原则
  - go-couchbase - Go中的Couchbase客户端
  - go-couchdb - Go的另一个CouchDB HTTP API包装器
  - gocb - 官方Couchbase Go SDK
  - gocql - Apache Cassandra的Go语言驱动程序。
  - gomemcache - Go编程语言的memcache客户端库。
  - gorethink - 转RethinkDB的语言驱动程序
  - goriak - Riak KV的语言驱动程序
  - mgo - 用于Go语言的MongoDB驱动程序，它根据标准Go语言在非常简单的API下实现丰富且经过良好测试的功能选择。
  - neo4j - Golang的 Neo4j Rest API绑定
  - Neo4j-GO - golang中的Neo4j REST客户端。
  - neoism - Golang的 Neo4j客户端
  - redigo - Redigo是Redis数据库的Go客户端。
  - redis - Golang的Redis客户端
  - redis - Go的一个简单，强大的Redis客户端。
  - redis - 兼容Redis协议的TCP服务器/服务。

- 搜索和分析数据库
  - bleve - 一个用于go的现代文本索引库。
  - elastic - Go的Elasticsearch客户端。
  - elastigo - Elasticsearch客户端库。
  - go - 与Elasticsearch交互的库。
  - skizze - 概率数据结构服务和存储。
  
收集至：https://github.com/gostor/awesome-go-storage
