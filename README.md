# 1. mongodb

* 下面这个查询可以找到所有温度和时间

```
{tags: {$nin: ["_grokparsefailure"]}}, {temp: 1, time: 1}
```

# 2. jdk11

# 3. logstash

* 下载安装logstash

```
https://www.elastic.co/downloads/logstash
```

* 安装mongo插件

```
logstash-plugin install logstash-output-mongodb
```

* 启动logstash
```
logstash -f pipeline.conf --config.reload.automatic
```

# 4. filebeat

* 把filebeat安装到日志所在的机器上

```
https://www.elastic.co/downloads/beats/filebeat
```

* 把filebeat.yml复制到该机器上。找到下面这行，把LOGSTASH_HOST改成logstash所在机器

```
output.logstash:
  # The Logstash hosts
  hosts: ["LOGSTASH_HOST:5044"]
```

* 找到下面这行，路径是filebeat监控的文件

```
filebeat.inputs:
- type: log
  enabled: true
  paths:
    - FULL\PATH\TO\LOG\*.log
```

* 启动filebeat

```
filebeat.exe -e -c filebeat.yml -d "publish"
```



