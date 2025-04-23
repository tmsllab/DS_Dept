# Start hadoop

```BASH
cd hadoop-3.4.1/etc/hadoop/
```

```BASH
ssh localhost
```

```BASH
ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa 
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

```BASH
chmod 0600 ~/.ssh/authorized_keys
```

```BASH
hadoop-3.4.1/bin/hdfs namenode -format
```

```BASH
export PDSH_RCMD_TYPE=ssh
```

```BASH
start-all.sh

```
Copy the bellow url and paste default browser(Firefox here)
```BASH
localhost:9870
```

Now choose the Utilities tab select the 1st option(Browse the file system)

when you update something on Hadoop it will shown here.


## To stop Hadoop System
```
stop-all.sh
```
