Dtoop
===

Dtoop Version 1.0 beta
Data to Hadoop, yet another Sqoop.

![设计逻辑]("逻辑设计")

PRE
---

- 安装MySQL客户端和Hadoop客户端，保证mysql命令和hdfs命令可用
- 主机到接收数据的MySQL服务器之间需要免密码登陆

INSTALL
---

- ADD the following to env:

```
export DTOOP_HOME=<path>
export PATH=$PATH:$DTOOP_HOME/bin
```

USAGE
---

### export-import
#### MySQL -> FILE

__TRUNCAT/CREATE FILE__

```
dtoop-import -u"root" -p"***" -h"172.17.0.54" -d"test" -q"select * from user" -o"/tmp/user"
```

__APPEND FILE__

```
dtoop-import -u"root" -p"***" -h"172.17.0.54" -d"test" -q"select * from user" -o"/tmp/user" -t" "
```

#### FILE -> HDFS 

```
dtoop-import -i"/tmp/user" --target-dir "hdfs://user/forevernull/user"
```


#### MySQL -> HDFS

```
dtoop-import -u"root" -p"***" -h"172.17.0.54" -d"test" -q"select * from user" \
-q"select * from user" -o"/tmp/user" --target-dir "hdfs://user/forevernull/user"
```

### dtoop-export
### FILE -> MySQL

```
dtoop-export -u"root" -p"***" -h"127.0.0.1" -d"test" --table "user" --input "/tmp/user" --target-host "172.17.0.54"
```

#### HDFS -> MySQL

```
dtoop-export -u"root" -p"***" -h"127.0.0.1" -d"test" --table "user" --input "/tmp/user" --target-host "172.17.0.54" --target-dir "hdfs://bi/user/forevernull/user"
```

#### HIVE Query -> FILE

```
dtoop-export --hive-query "select * from default.user" --target-dir "/tmp/user"  -i"/tmp/user" --to-file " "
```
#### HIVE Query -> MySQL

```
dtoop-export -u"root" -p"***" -h"127.0.0.1" -d"test" --table "user" --hive-query "select * from default.user" --target-dir "/tmp/user"  -i"/tmp/user" --target-host "172.17.0.54"
```
