本文为您介绍 TDSQL-C MySQL 版内核版本更新动态，如需升级，请参见 [升级内核小版本](https://intl.cloud.tencent.com/document/product/1098/44617)。

## TDSQL-C MySQL 版 8.0
### 3.1.3
#### 功能更新
- 支持将指定 filename 的 binlog 加入到 index 文件中。
- 新增 backup 锁，语法 LOCK TABLES FOR BACKUP，UNLOCK TABLES。
- 新增 binlog 锁，语法 LOCK BINLOG FOR BACKUP，UNLOCK BINLOG。

#### 问题修复
- 修复动态元信息持久化导致实例表损坏或可见性错误的 bug。
- 合入官方 bugfix Bug #32897503，解决 prepare 语句下，部分查询语句执行路径错误的问题。
- 合入官方 bugfix：set resource group 失败会 crash 的问题。
- 修复 HA 切换后 previous gtid 为空的 bug。
- 修复自增列可设置为小于已插入最大值的 bug。
- 修复只读实例上的显式事务会阻塞回放线程回放 DDL 日志。
- 修复表名中存在"-"的表 DDL 后在只读实例上复制可能会 crash 的问题。
- 修复只读实例启动遇到 DDL recover 导致操作 DDL log 系统表申请 undo 时 crash 的问题。

### 3.1.2
#### 功能更新
- 支持 MySQL 8.0，增加只读节点，主备物理复制。
- 支持扩展表空间，实例容量最大支持1PB+容量。
- 支持预加载行数限制功能 ，在点查询相关测试中，得到了1~5%的性能提升。
- 支持扩展 ANALYZE 语法（UPDATE HISTOGRAM c USING DATA 'json'），支持直接写入直方图功能。

#### 性能优化
- 使用直方图替代索引下探，降低评估误差以及 I/O 开销，该能力默认未打开。

#### 问题修复
- 修复创建包含大对象列的全文索引时，大对象页相关更新没有写日志的问题。
- 修复计算和存储层 undo page 格式不一致的问题，TRX_UNDO_HISTORY_NODE 定义不一样。
- 修复 online-DDL 期间统计信息可能为零的情况。
- 修复从机 generated column 不更新的情况。
- 修复 binlog 压缩时实例 hang 住的问题。
- 修复新产生的 binlog 文件的 previous_gtids event 中的 gtid 缺失问题。
- 修复修改系统变量时可能死锁的问题。
- 修复 show processlist 中从机 sql 线程的 info 显示不正确的问题。
- 移植官方8.0.23中 hash join 相关的 bugfix。
- 移植官方 writeset 相关 bugfix。
- 移植官方8.0.24中查询优化器相关的 bugfix。
- 修复 FAST DDL 中优化 flush list 释放页面并发 bug。
- 优化海量个数表的实例升级数据字典时占用大量内存。
- 修复 instant add column 后在创建新主键场景下的 crash 问题。
- 修复全文索引查询中内存增长导致 OOM 问题。
- 修复 show processlist 返回结果集中 TIME 字段出现-1的问题。
- 修复直方图兼容性可能导致表无法打开的问题。
- 修复构建 Singleton 直方图的浮点累加误差。
- 修复 row 格式日志时表名为较长的中文字符导致复制中断问题。

### 3.1.1
#### 功能更新
- 合并官方 8.0.19、8.0.20、8.0.21、8.0.22 变更。
- 支持动态设置 thread_handling 线程模式或连接池模式。
- 支持主从 bp 同步功能：当发生 HA 并进行主备切换后，备库通常需要一段比较长的时间来 warmup，把热点数据加载到buffer pool。为加速备机的预热，TXSQL 支持了主从 bp 同步功能。
- 支持 Sort Merge Join 功能。
- 支持异步提交，当打开线程池和关闭 binlog 时设置参数 innodb_log_sync_method =async 即可以开启异步提交。
- 支持 FAST DDL 功能。
- 支持用户侧查询 character_set_client_handshake 参数显示当前值功能。
- 支持数据库审计。

#### 性能优化
- 优化扫描 flush list 刷脏：通过优化刷脏机制，解决了创建索引过程中的性能抖动问题，提升了系统稳定性。
- 优化 BINLOG LOCK_done 锁冲突，提升写入性能。
- 使用 Lock Free Hash 优化 trx_sys mutex 冲突，提升性能。
- redo log 刷盘优化。
- buffer pool 初始化时间优化。
- 大表 drop table 清理 AHI 优化。

#### 问题修复
- 修复修改 offline_mode、cdb_working_mode 参数的死锁问题。
- 修复 trx_sys的max_trx_id 持久化并发问题。
- 修复清理 innodb 临时表时造成的性能抖动问题。
- 修复核数较多的实例 read only 性能下降的问题。
- 修复 hash scan 导致1032问题。
- 修复热点更新功能的并发安全问题。

### 3.0.1
#### 功能更新
- 支持 cynos_version，通过三种方式查询 select CYNOS_VERSION()、select @@cynos_version、show variables like 'cynos_version'。
- 增加空间限制参数，总空间超过限制时扩展的更新会报错，警告提示用户释放空间或者升级规格。
- 增加只读参数 innodb_ncdb_log_priority，表示主实例后台日志线程优先级。
- 增加只读参数 innodb_ncdb_apply_priority，表示只读实例日志回放线程优先级。
- 增加动态参数 innodb_ncdb_fast_shutdown，控制进程是否快速 shutdown，开启之后进程退出将不再做一些全局结构的析构操作，缩短 shutdown 时间，默认关闭。
- 增加参数 innodb_max_temp_data_file_size，只读参数，默认值128M，当此参数大于0时，代表本地存储中最大可以容纳的临时表空间。

## TDSQL-C MySQL 版 5.7
### 2.0.17
#### 功能更新
- 支持将指定 filename 的 binlog 加入到 index 文件中。

#### 问题修复
- 合入官方 bugfix BUG#25865525，解决 LOAD DATA INFILE 读入转义字符加 utf8 字符失败的问题。

### 2.0.16
#### 特性更新
- 优化 undo space truncate，提升大规格实例 undo truncate 速度。
- 优化只读实例上大范围查询的性能。

#### 问题修复
- 修复 backup lock 受 lock table 语句影响无法加锁备份的问题。
- 修复 instant add 上千列后，RO 出现 table share 错乱的问题。
- 修复 binlog 的内容包含转义关键字回放报错的问题。
- 修复外部 prepared XA 事务不显式回滚阻塞正常 shutdown 的问题。
- 修复只读实例启动过程中报 warning“tablespace -1 not found” 警告的问题。

### 2.0.15
#### 功能更新
- 支持扩展表空间，当单个表空间超过 innodb_ncdb_extend_space_threshold 配置新表会创建到扩展表空间中。
- JSON 新增函数 JSON_MERGE_PRESERVE ，JSON_MERGE_PATCH，JSON_PRETTY，JSON_STORAGE_SIZE，JSON_ARRAYAGG，JSON_OBJECTAGG。
- 优化系统启动时表锁恢复流程，缩短启动时间。

#### 问题修复
- 修复官方 bugfix，包含 text 列 group by 性能问题和多个虚拟列相关的问题。
- 修复实例启动后大事务回滚与 shutdown 操作并发时，可能导致实例 crash 的问题。
- 修复 undo space truncate 失败重试时相关页面 io 重试多次失败，导致实例退出的问题。
- 修复只读实例关闭时统计信息更新访问快照缓存，导致 crash 的问题。
- 修复 undo space truncate 可能存在 truncate log 落后于 truncate 操作的问题。
- 修复官方 bugfix，分区表扫描 ICP 检查错误，导致查询慢的问题。
- 修复只读实例中前项扫描遇到索引分裂日志部分回放，导致 crash 的问题。

### 2.0.14
#### 功能更新
- 支持 instant modify column，使用请参见 [Instant DDL 功能介绍](https://intl.cloud.tencent.com/document/product/1098/44589)。

#### 问题修复
- 修复只读实例中临时表删除时，占用空间不回收的问题。
- 修复只读实例因为存储路由变更读到老的页面版本，导致退出的问题。
- 修复查询 information_schema.metadata_locks 时，可能发生的 crash 问题。
- 修复只读实例前向扫描与 btree SMO 的并发问题。
- 修复当多表出现复杂外键依赖，且外键属性为 ON DELETE CASCADE，在 DELETE 父表记录时可能导致子表对应的记录被删除两次的问题。
- 修复只读实例 create user 等相关操作，导致退出的问题。
- 修复只读实例中 show volume status，可能触发断言失败的问题。
- 修复分区表频繁 DDL 后，只读实例查询结果异常和 crash 的问题。
- 修复只读实例查询扫描到已经被 purge 的 undo log，导致构造历史版本 crash 的问题。

### 2.0.13
#### 功能更新
- 支持 instant add column，使用请参见 [Instant DDL 功能介绍](https://intl.cloud.tencent.com/document/product/1098/44589)。
- 优化高负载下的审计性能，增加动态参数 lock_usleep_time。

#### 问题修复
- 修复官方针对 dict_operation_lock 在外键检查中可能引起的死锁问题。
- 修复只读实例启动阶段回放 acl change 日志，可能导致退出的问题。
- 修复 instant add column 和 truncate table 后，主从数据不一致的问题。
- 修复 instant add column 和 truncate table 后，再次插入数据导致日志回放错误的问题。
- 修复创建包含 instant add column 列的主键，导致退出的问题。
- 修复使用 instant column 新建 partition，rebuild partition，只读实例查询表结构退出的问题。

### 2.0.12
#### 功能更新
- 支持数据库审计，使用请参见 [开通 TDSQL-C MySQL 版审计](https://intl.cloud.tencent.com/document/product/1102/41312)。
- 支持 purge 页面预读，加快空间回收速度。
- 实时更新系统视图中表和索引大小信息。
- 增加额外的线程用以加快推进 recycle lsn，加快存储的 GC。

#### 问题修复
- 修复全文索引官方 BUG，包括：BUG#24938374，BUG#21625016，BUG#27082268，BUG#27155294，BUG#27326796，BUG#27304661，BUG#25289359，BUG#29717909，BUG#30787535。
- 修复官方 BUG，涉及并发更新可能导致系统 crash，包括 BUG#30950714、BUG#31205266、BUG#25669686。
- 修复官方 BUG#28104394，未提交的插入操作会影响索引建的 range scan，使其返回错误的行数。
- 修复官方 BUG#30488700，derived table 查询计划有误导致性能差的问题。
- 修复主机执行 DDL 后，只读实例回放统计信息日志可能导致退出的问题。
- 修复 rename table 到不存在 DB 的问题。
- 修复主机 optimize table，导致只读实例可能退出的问题。
- 修复全文索引表的更新在只读实例存在事务一致性的问题。
- 修复 set offline mode 和 show variables 操作发生死锁的问题。

### 2.0.11
#### 功能更新
- 优化 binlog 文件索引，提升扫描 binlog 文件的速度。
- 优化 shutdown 流程，提升 shutdown 速度。
- 优化实例内存，压缩 buffer zip hash 等结构的内存占用。
- 优化只读实例启动时恢复 DDL lock 的流程，加快回放速度。
- 优化只读实例 load 系统表的流程，加快启动速度。
- 优化 purge coordinator 工作线程分配，提升 purge 速度。

#### 问题修复
- 修复 index 结构映射错误，导致的 open table 时挂掉的问题。
- 修复 xa 事务回滚时，在只读实例复制出现异常的问题。
- 修复在只读实例中启动 binlog 复制，导致启动 crash 的问题。
- 修复 flush logs 导致的内存泄漏问题。
- 修复 mysqladmin shutdown 无法退出的问题。
- 修复主机 drop column时，只读实例连接无法回放日志的问题。
- 修复插入 blob 大对象触发空间限制后，依然可以灌数的问题。
- 修复主机大表 DDL 和日志写盘慢，可能导致的只读实例复制可用性问题。
- 修复临时表设置 innodb_max_temp_data_file_size 后，存储浪费小表的问题。

