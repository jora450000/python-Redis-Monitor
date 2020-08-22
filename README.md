  convert script to python3
  translate  to english
  
# simple python script to monitor redis performance


[Previous article](http://blog.51cto.com/legehappy/2145967) has already talked about how to monitor memcached, and now also how to monitor redis by the way.

## First introduce the information of monitoring redis:
* Redis ping: check ping
* Redis alive: Check whether the port is alive
* Redis connections: view the number of connections
* Redis blockedClients: the number of blocked clients waiting
* Redis connectionsUsage: Redis connection usage rate
* Redis memoryUsage: Redis memory usage
* Redis memoryUsageRate: redis memory usage rate
* Redis evictedKeys: The number of keys deleted since the operation
* Redis rejectedConnections: the number of rejected connections
* Redis ops: OPS of redis
* Redis hitRate: redis hit rate
```
pip3 install redis
```


43/5000
### Test script to view and monitor redis information (if redis has not set a password, it can be executed without a password):

``` 
/bin/python3 /home/python/check_redis.py test 192.168.4.18 6379 password
Redis ping: True
Redis alive: 0
Redis connections: 447
Redis blockedClients 0
Redis connectionsUsage: 4.47%
Redis memoryUsage: 2885122048
Redis memoryUsageRate: 17.32%
Redis evictedKeys: 0
Redis rejectedConnections: 0
Redis ops: 1050
Redis hitRate: 71.87%
```

### Finally added to the zabbix custom key

```
cat /etc/zabbix/zabbix_agentd.d/redis.conf
# Redis
UserParameter=redis.stats[*],/bin/python3 /home/python/check_redis.py $1 192.168.4.18 6379 password
```
