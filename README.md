Dtoop
===

Dtoop Version 1.0 beta
Data to Hadoop, yet another Sqoop.

![what it do](https://cloud.githubusercontent.com/assets/7134102/19676744/7e37be40-9ac8-11e6-8ab2-d97db8ea89b8.png "what it do")

PREPARE
---

- MySQL and HADOOP Client NEEDED!
- [SSH Authorized v2](http://sshkeychain.sourceforge.net/mirrors/SSH-with-Keys-HOWTO/SSH-with-Keys-HOWTO-4.html)

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
- MySQL -> FILE

    + TRUNCAT/CREATE FILE
```
dtoop-import -u"root" -p"***" -h"172.17.0.54" -d"test" -q"select * from user" -o"/tmp/user"
```

    + APPEND FILE
```
dtoop-import -u"root" -p"***" -h"172.17.0.54" -d"test" -q"select * from user" -o"/tmp/user" -t" "
```

- FILE -> HDFS 
```
dtoop-import -i"/tmp/user" --target-dir "hdfs://user/forevernull/user"
```

- MySQL -> HDFS
```
dtoop-import -u"root" -p"***" -h"172.17.0.54" -d"test" -q"select * from user" \
-q"select * from user" -o"/tmp/user" --target-dir "hdfs://user/forevernull/user"
```

### dtoop-export
- FILE -> MySQL
```
dtoop-export -u"root" -p"***" -h"127.0.0.1" -d"test" --table "user" \
--input "/tmp/user" --target-host "172.17.0.54"
```

- HDFS -> MySQL
```
dtoop-export -u"root" -p"***" -h"127.0.0.1" -d"test" --table "user" \
--input "/tmp/user" --target-host "172.17.0.54" --target-dir "hdfs://bi/user/forevernull/user"
```

- HIVE Query -> FILE
```
dtoop-export --hive-query "select * from default.user" --target-dir "/tmp/user"  -i"/tmp/user" --to-file " "
```

- HIVE Query -> MySQL
```
dtoop-export -u"root" -p"***" -h"127.0.0.1" -d"test" --table "user" \
--hive-query "select * from default.user" --target-dir "/tmp/user"  -i"/tmp/user" --target-host "172.17.0.54"
```
