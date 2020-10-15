```flow
start=>start: 创建时

constructor=>operation: constructor
cached=>condition: 是否有缓存？
sendMq=>operation: 发送MQ，后台服务更新缓存
info=>operation: 读取信息
setCache=>operation: 保存缓存
end=>end: 返回信息

start->constructor->cached
cached(yes)->sendMq
cached(no)->info
info->setCache
setCache->end
sendMq->end
```