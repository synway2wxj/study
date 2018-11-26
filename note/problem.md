# 定时任务集群环境部署
如何限定只有一台机器在执行定时任务
某台服务宕机以后如何进行故障转移
如何确定正在执行的是哪一台服务
* 利用mysql的排他锁
* quartz集群需要数据库的支持（JobStore TX或者JobStoreCMT），从本质上来说，是使集群上的每一个节点通过共享同一个数据库来工作的；在\docs\dbTables下选择合适你数据库的SQL执行文件，创建quartz集群需要的表
quartz
quartz-jobs 
https://www.liangzl.com/get-article-detail-718.html
* 固定执行定时任务的机器
在数据库建立多张表，从定时任务表中获取定时方法
借助Redis的过期机制和分布式锁
Quartz的集群应用方式
Springboot 集成 quartz为什么非要集成呢, 因为quartz支持集群定时任务, 现在还用不到, 防止以后用到
