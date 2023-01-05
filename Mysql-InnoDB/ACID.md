# ACID

## 介绍

A: atomicity.

C: consistency.

I:: isolation.

D: durability.

## Atomicity

ACID 模型的原子性方面主要涉及 InnoDB 事务。相关的 MySQL 特性包括
* The autocommit setting.
* The COMMIT statement.
* The ROLLBACK statement.

## Consistency

ACID 模型的一致性方面主要涉及内部 InnoDB 处理以保护数据免于崩溃。相关的 MySQL 特性包括：

* InnoDB [双写缓冲区](https://dev.mysql.com/doc/refman/8.0/en/innodb-doublewrite-buffer.html)
* InnoDB [崩溃恢复](https://dev.mysql.com/doc/refman/8.0/en/innodb-recovery.html#innodb-crash-recovery)

## Isolation

ACID 模型的隔离方面主要涉及 InnoDB 事务，特别是应用于每个事务的隔离级别

* 自动提交(auto commit)设置
* 事务隔离级别和 SET TRANSACTION 语句。 请参阅第 15.7.2.1 节，“[事务隔离级别](https://dev.mysql.com/doc/refman/8.0/en/innodb-transaction-isolation-levels.html)”。
* InnoDB 锁定的底层细节。 可以在 INFORMATION_SCHEMA 表（参见第 15.15.2 节，[“InnoDB INFORMATION_SCHEMA 事务和锁定信息](https://dev.mysql.com/doc/refman/8.0/en/innodb-information-schema-transactions.html)”）和 Performance Schema data_locks 和 data_lock_waits 表中查看详细信息。

## Durability

ACID 模型的持久性方面涉及与特定硬件配置交互的 MySQL 软件功能。 由于有多种可能性取决于您的 CPU、网络和存储设备的能力，因此在这方面提供具体指导方针是最复杂的。

* InnoDB [双写缓冲区](https://dev.mysql.com/doc/refman/8.0/en/innodb-doublewrite-buffer.html)
* innodb_flush_log_at_trx_commit 变量。
* sync_binlog 变量。
* innodb_file_per_table 变量。
* 还受到操作系统及环境、硬件缓冲、硬件供电、备份策略等影响