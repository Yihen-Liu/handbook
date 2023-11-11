#### Redis配置

>  vim /etc/redis/redis.conf

##### 1. 设置密码

```
requirepass your-password
```



#### Redis-cli客户端命令

##### 1. 连接server

```
# redis-cli -h 192.168.1.1 -p 6379
连接成功后，如果配置文件里设置了密码，需要在交互界面执行如下内容，才可以进行后续操作：
> auth password
```

##### 2. 退出

```
> quit/exit
```

##### 3. 切换DB

```
> select 10   # 切换到10号DB，默认是0号DB
```

##### 4. 查看当前数据库容量

```
> dbsize
```

##### 5. 查看redis信息

```
> info
```





#### References

1. [Redis cli命令](https://www.cnblogs.com/kongzhongqijing/p/6867960.html)