# CloudDBA简介 {#concept_wpx_tqn_wdb .concept}

CloudDBA是监控和管理RDS实例性能及运行状况的服务，在RDS控制台的实例管理页面，目前适用于 MySQL 5.6、PostgreSQL 10、PPAS 10 版本的实例。针对SQL语句的性能、CPU使用率、IOPS使用率、内存使用率、磁盘空间使用率、连接数、锁信息、热点表等，CloudDBA提供了智能的诊断及优化功能，能最大限度发现数据库存在的或潜在的健康问题。CloudDBA的诊断基于单个实例，该诊断会提供问题详情及相应的解决方案，可为您管理实例运行状况带来极大的便利。

## 功能介绍 {#section_h5s_wqn_wdb .section}

CloudDBA主要包含如下功能：

-   智能优化：提供实例性能监控和综合评分的概况，主要如下4个部分构成。

    -   实例基本信息：CloudDBA所监控和诊断的实例ID、类型、所在地域和可用区、链路类型等。

    -   [查看实例运行状况](cn.zh-CN/用户指南/CloudDBA数据库性能优化/智能优化/查看实例运行状况.md#)：提供了活跃线程、慢SQL、网络流量和锁状态的监控图，该数据每5秒刷新一次，如下图所示（本文图示仅为示例，请以实际界面为准）。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7899/3051_zh-CN.png)

    -   实例核心资源使用率：显示了实例当前CPU、内存、连接数、IOPS和磁盘空间的使用率，该数据每20秒刷新一次，如下图所示（本文图示仅为示例，请以实际界面为准）。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7899/3051_zh-CN.png)

    -   [诊断实例性能](cn.zh-CN/用户指南/CloudDBA数据库性能优化/智能优化/诊断实例性能.md#)：显示实例性能的诊断评分和诊断结果。系统不会自动进行诊断，您需要手动进行一键诊断，如下图所示（本文图示仅为示例，请以实际界面为准）。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7899/3053_zh-CN.png)

-   问题诊断：提供实例诊断详情，包括CPU、空间、慢SQL、锁信息、热点表和诊断历史，详情如下所示。

    -   [诊断和终止实时会话](cn.zh-CN/用户指南/CloudDBA数据库性能优化/问题诊断/诊断和终止实时会话.md#)：显示CPU、内存和IOPS的使用状态，以及当前实例的实时会话列表。另外，您还可以诊断会话并查询诊断历史。

    -   [查看空间使用详情](cn.zh-CN/用户指南/CloudDBA数据库性能优化/问题诊断/查看空间使用详情.md#)：显示当前实例数据空间和日志空间的使用状态，以及数据库中所有表的详情。

    -   [诊断慢SQL](cn.zh-CN/用户指南/CloudDBA数据库性能优化/问题诊断/诊断慢SQL.md#)：诊断当前实例最近1个月内的慢SQL，并给出慢SQL的优化建议。

    -   [诊断锁信息](cn.zh-CN/用户指南/CloudDBA数据库性能优化/问题诊断/诊断锁信息.md#)：诊断当前实例的锁、事务和死锁。

    -   [诊断热点表](cn.zh-CN/用户指南/CloudDBA数据库性能优化/问题诊断/诊断热点表.md#)：诊断当前实例的热点表和热点索引。

    -   [查看诊断历史](cn.zh-CN/用户指南/CloudDBA数据库性能优化/问题诊断/查看诊断历史.md#)：您可以查看所有类型的诊断历史及诊断详情。

-   SQL操作：系统可以根据您输入的SQL语句给出诊断优化意见。

-   [分析SQL和会话事务](cn.zh-CN/用户指南/CloudDBA数据库性能优化/分析SQL和会话事务.md#)：显示特定时间段内实例CPU和IOPS的状况，并对历史SQL进行分析。

-   [查看和下载实例性能诊断报告](cn.zh-CN/用户指南/CloudDBA数据库性能优化/查看和下载实例性能诊断报告.md#)：您可以创建、查看和下载实例的诊断报告。诊断报告生成时间大约需要10分钟左右，诊断报告列表中可显示最近30天内的报告数据。


## 功能限制 {#section_qhg_yqn_wdb .section}

目前，CloudDBA仅适用于公共云华北1、华北2、华东1、华东2、华南1地域的MySQL类型的实例。

## 最佳实践 {#section_d4c_zqn_wdb .section}

[利用CloudDBA解决MySQL实例CPU使用率过高的问题](https://help.aliyun.com/document_detail/65233.html)

