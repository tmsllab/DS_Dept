# Start hadoop

```BASH

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
